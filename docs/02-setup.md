# 02 - setting it all up

im reusing the wazuh setup from my detection lab so i wont repeat that here. this doc is mostly about adding thehive and shuffle.

## vms

| vm | whats on it | ram |
|----|----|----|
| wazuh | wazuh manager (already had this) | 4gb |
| thehive | thehive + cassandra + elasticsearch | 4gb (needs it, thehive is hungry) |
| shuffle | shuffle (runs in docker) | 2gb |

note: thehive needs cassandra AND elasticsearch to run which i did not expect. it ate all my ram at first. had to bump the vm up.

## thehive

thehive has a docker-compose setup which is the easiest way. on the thehive vm (needs docker + docker compose):

```bash
git clone https://github.com/StrangeBeeCorp/docker.git thehive-docker
cd thehive-docker/testing
docker compose up -d
```

wait a bit then open http://<thehive-ip>:9000
default login is admin@thehive.local / secret (CHANGE THIS obviously)

took me a couple tries, first time elasticsearch wouldnt start - had to set vm.max_map_count:

```bash
sudo sysctl -w vm.max_map_count=262144
```

## shuffle

shuffle also runs in docker:

```bash
git clone https://github.com/Shuffle/Shuffle
cd Shuffle
docker compose up -d
```

then http://<shuffle-ip>:3001, make an admin account.

## whats next

now the pieces exist but they dont talk to each other yet. thats the next two docs:
- wazuh -> thehive so alerts become cases
- shuffle in the middle to automate

next: [03 - connect wazuh to thehive](03-connect-wazuh-thehive.md)
