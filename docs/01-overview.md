# 01 - what even is a SOC

writing down what i learned so it sticks.

a SOC (security operations center) is basically the team/place that watches for attacks and responds to them. analysts sit and look at alerts all day and decide "is this real or noise".

the part i didnt get at first: detecting an attack is only step 1. theres a whole process after:

1. **alert** - the SIEM (wazuh) notices something
2. **triage** - analyst looks at it. real threat or false alarm?
3. **case** - if its real, open a case (in thehive) to track it
4. **investigate** - gather more info. who, what, when. enrich it (lookup the ip/hash)
5. **respond** - contain it, e.g. block the ip, disable the account
6. **close** - write down what happened

## tiers

apparently SOCs have tiers:
- tier 1 = triage, the first look, closes easy stuff
- tier 2 = deeper investigation
- tier 3 = threat hunting, the pros

im basically practicing being a tier 1 that also builds the automation.

## why automate (SOAR)

analysts get flooded with alerts. a lot of the work is repetitive - copy the ip, paste into virustotal, check if its bad, write it in the case. boring and slow.

SOAR (shuffle here) does that automatically. so when an alert comes in the ip is already checked and the result is sitting in the case waiting for me. that lets a small team handle way more.

thats the whole point of this lab - build that pipeline myself so i understand it.

next: [02 - setup](02-setup.md)
