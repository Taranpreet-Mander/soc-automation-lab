# IR runbook - brute force login

what to do when wazuh alerts on a brute force (lots of failed logins). IR = incident response.
mapped to MITRE T1110.

## 1. confirm its real

- check the alert: many 4625 (windows) or failed ssh, short time, same source ip = yes its a brute force attempt.
- how many attempts? from where?

## 2. did it SUCCEED? (most important question)

look for a successful login (4624 / accepted ssh) from the same ip right after the failures.
- no success -> attempted only, less urgent
- success -> this is now a real intrusion, bump to HIGH, this is the scary path

## 3. contain

- block the source ip (firewall). in my lab shuffle will eventually do this automatically, for now i do it by hand.
- if an account was compromised: disable it / force password reset.

## 4. investigate (if it succeeded)

- what did they do after logging in? check process logs (this is where my sysmon setup from the other lab helps).
- did they create users, run commands, move to other machines?

## 5. recover

- remove anything they added, reset creds, patch the way they got in (weak password? RDP exposed?).

## 6. lessons

- write down how they got in and what would have stopped it (account lockout policy, strong passwords, mfa, not exposing RDP).

## notes to self

in my lab so far ive only done the "attempt, no success" version. want to try the full compromise path next where i actually let it succeed and then trace what happened.
