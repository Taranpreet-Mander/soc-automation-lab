# triage checklist

when an alert fires this is the order i go through. basically deciding: real or false alarm, and how bad.

## 1. read the alert

- what rule fired? what level?
- what machine (host)?
- what time? one off or repeating?

## 2. is it a false positive?

- is this normal activity for that machine? (e.g. an admin script vs an attacker)
- has this alert fired a lot before and always been nothing?
- if clearly nothing -> close it, note why.

## 3. enrich (get more context)

- source ip - internal or external? is it known bad? (shuffle should have already done the virustotal lookup and stuck it on the case)
- the user account involved - is it a normal user, admin, or service account?
- any related alerts around the same time?

## 4. decide severity

rough rule i use:
- low = suspicious but no impact (one failed login)
- medium = repeated / targeted (brute force attempt)
- high = looks successful (login AFTER the brute force, or malware ran)

## 5. escalate or handle

- if its beyond me -> escalate (in a real SOC to tier 2). in my lab i just note "would escalate".
- if i can handle it -> follow the specific runbook (like the brute force one).

## 6. document

write in the thehive case: what it was, what i found, what i did, closed or escalated. future me will thank present me.

the point of a checklist is to not skip steps when youre tired or its 3am.
