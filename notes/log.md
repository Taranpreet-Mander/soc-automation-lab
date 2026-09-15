# log

notes as i build this. newest on top.

---

## fighting with shuffle conditions

the enrichment (virustotal lookup) works and shows up nicely. but i cannot get the IF condition to branch on the score. i think im comparing a string to a number or the path is wrong. printed everything to debug, still stuck. leaving it making a case both ways for now and moving on before i lose my mind.

small win: got the discord notification working, felt cool to get pinged by my own SOC.

---

## alerts reaching thehive

wazuh -> shuffle -> thehive full chain worked today!! took a while:
- level filter was too high so my test alerts werent being sent
- thehive api key auth in shuffle - had it in the wrong field first

seeing a real failed-login alert turn into a thehive case automatically was very satisfying.

---

## thehive is heavy

did not realise thehive needs cassandra + elasticsearch. it crashed my vm from lack of ram. bumped it to 4gb and set vm.max_map_count for elasticsearch and it came up. shuffle was easier, just docker compose.

---

## day 1 - planning

decided to build a SOC automation lab as a step up from my detection lab. that one was about MAKING alerts, this one is about what you DO with them + automating it.

plan: wazuh (already have it) -> thehive for cases -> shuffle to automate.
goal is to actually understand SOAR by building one, not just reading about it.

still fuzzy on how much of shuffle i need to learn. gonna learn by doing.
