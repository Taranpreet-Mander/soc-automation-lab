# 03 - connect wazuh to thehive (via shuffle)

goal: when wazuh makes an alert, it ends up as a case in thehive. i decided to route it THROUGH shuffle instead of wazuh talking to thehive directly, because then shuffle can enrich it on the way (next doc).

so the real flow is: wazuh -> shuffle -> thehive.

## step 1 - wazuh sends alerts to shuffle

wazuh can run an "integration" that fires on alerts. shuffle gives you a webhook url. so i point wazuh at that webhook.

on the wazuh manager, edit /var/ossec/etc/ossec.conf and add an integration block:

```xml
<integration>
  <name>shuffle</name>
  <hook_url>http://<shuffle-ip>:3001/api/v1/hooks/webhook_XXXXX</hook_url>
  <level>7</level>
  <alert_format>json</alert_format>
</integration>
```

the level 7 means "only send me alerts level 7 and up" so it doesnt spam shuffle with every tiny thing. i started higher (level 10) while testing so i didnt drown.

restart wazuh: sudo systemctl restart wazuh-manager

## step 2 - grab the webhook in shuffle

in shuffle, make a new workflow, drag a "Webhook" trigger onto it, and it gives you the url. thats what goes in the hook_url above. start the webhook.

## step 3 - test

trigger an alert (i just did a bunch of failed ssh logins). check shuffle - the "executions" should show the alert coming in as json. 

first time nothing showed up. turned out my level filter was too high and my test alert was only level 5. lowered it and it worked.

## step 4 - shuffle creates the thehive case

in the workflow, add a TheHive app node after the webhook, set it to "create alert" (or create case), and map the fields from the wazuh json - title, description, source ip etc. you need thehives api key for this (Settings -> API key in thehive), store it in shuffle as an "authentication", NOT hardcoded.

now an alert flows all the way to a thehive case on its own. still a bit flaky - sometimes the field mapping breaks if the wazuh alert has a weird shape. noted in my log.

next: [04 - the shuffle automation](04-shuffle-automation.md)
