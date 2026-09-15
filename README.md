# SOC Automation Lab

building a mini SOC (security operations center) at home to learn how analysts actually work - not just detecting stuff but the whole workflow after an alert fires. triage it, open a case, and automate the boring parts.

still learning, this is a work in progress. writing everything down so i remember.

(this is a follow up to my other repo where i just did detections - this one is more about what happens AFTER the alert.)

## the idea

an alert should flow through the whole pipeline automatically:

```
wazuh (SIEM, makes the alert)
        |
        v
thehive (case management - turns alerts into cases i can work)
        |
        v
shuffle (SOAR - automates enrichment, like looking up an ip/hash, and sends me a notification)
```

so instead of me manually copy pasting IPs into virustotal, shuffle does it and attaches the result to the case. thats the "automation" part.

## tools

- Wazuh - the SIEM (already know this from my last lab)
- TheHive - case management, where analysts track incidents
- Shuffle - the SOAR, does the automation workflows
- VirtualBox for the vms

## docs (writing as i go)

- [01 - what even is a SOC](docs/01-overview.md)
- [02 - setting it all up](docs/02-setup.md)
- [03 - connect wazuh to thehive](docs/03-connect-wazuh-thehive.md)
- [04 - the shuffle automation](docs/04-shuffle-automation.md)

## playbooks

the step by step guides an analyst follows:
- [triage checklist](playbooks/triage-checklist.md)
- [brute force IR runbook](playbooks/ir-bruteforce.md)

## todo

- [ ] get thehive receiving alerts reliably (works but flaky)
- [ ] finish the virustotal enrichment workflow in shuffle
- [ ] add a workflow that auto-blocks an ip (scary, doing this last)
- [ ] write more playbooks

## note

all in an isolated lab on my own vms. dont do security stuff to systems you dont own.

MIT license.
