# workflow: enrich and alert

writing down what my main shuffle workflow does, in plain english, so i (or anyone) can rebuild it. i didnt export the json yet because its still changing.

## trigger

webhook - receives the wazuh alert as json.

## steps

1. **webhook** receives alert
2. **extract fields** - pull out `data.srcip`, the rule description, the level, the agent name
3. **virustotal lookup** on the src ip -> get number of malicious detections
4. **(WIP) condition** - if malicious count > 0 then "bad path" else "normal path"
5. **create thehive case** with all the info + the virustotal result attached
6. **discord notify** - send me a message with a summary

## example (what a finished run looks like)

```
alert: sshd brute force, level 10
src ip: 203.0.113.55   (example ip)
virustotal: 6/89 engines flagged it as malicious
-> created thehive case #14, severity HIGH
-> pinged discord
```

## status

- steps 1,2,3,5,6 work
- step 4 (the branching) is the broken one, see docs/04
- next: export the workflow json and save it here so its reproducible
