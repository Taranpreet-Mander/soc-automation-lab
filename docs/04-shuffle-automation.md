# 04 - the shuffle automation (SOAR part)

this is the cool part and also the part im still fighting with. the idea: when an alert comes in, before making the case, automatically look up the suspicious ip/hash so i dont have to.

## the workflow so far

```
webhook (alert from wazuh)
   |
   v
pull out the source ip from the json
   |
   v
virustotal - is this ip known bad?
   |
   v
if bad -> make thehive case marked HIGH + send me a discord message
if unknown -> make normal case
```

## getting the ip out

the wazuh json is nested. the source ip for an ssh alert is around:
`data.srcip`

in shuffle you reference it like `$exec.text.data.srcip` (took me forever to get the path right, i printed the whole json to a repeat node to find it).

## virustotal node

- need a virustotal api key (free one, but its rate limited to like 4 lookups a min so dont hammer it)
- store the key in shuffle authentications, not in the workflow text
- feed it the ip, it returns how many engines flagged it

## the notify part

added a discord webhook so when something is HIGH it pings me. felt very "real SOC".

## whats broken / TODO

- the "if bad vs unknown" branching (shuffle conditions) - i cant get the condition to read the virustotal score properly yet. right now it makes a case either way. WIP.
- want to add a hash lookup too, not just ip
- the auto-block-ip idea is last because if i get it wrong i lock myself out of the victim lol

## what i learned

honestly the biggest thing: automation is mostly about getting the data mapping right between tools. each tool has its own json shape and half the battle is matching fields. once thats sorted the actual "logic" is simple.
