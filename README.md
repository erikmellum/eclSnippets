# Snippets & References

---
## Deployment

#### ISE
```bash
vagrant ssh
cd ecl
fab package:cloudlab
fab --host=54.149.66.159 --user=ubuntu deploy_restart:cloudlab, release_master_1231
```
#### Rosetta
```bash
vagrant ssh
cd ecl
fab package:rosettajs
fab --host=54.149.66.159 --user=ubuntu deploy_restart:rosettajs, release_master_1231
```
---
## Quick References

##### Rosetta Domain

* [Rosetta Dev](https://rjs-dev.emeraldcloudlab.com)
* [Rosetta Production](https://rosetta.emeraldcloudlab.com)

##### ISE Domain

* [ECL Dev](https://ise-dev.emeraldcloudlab.com)
* [ECL Production](https://ise.emeraldcloudlab.com)

#### SSH

* **Adding SSH Keys**
```bash
ssh-keygen -t rsa -C "erik@gmail.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
pbcopy < ~/.ssh/id_rsa.pub
```
* **Adding SSH Keys**
```bash
cat ~/.ssh/id_rsa.pub | ssh username@x.x.x.x 'cat >> .ssh/authorized_keys'
```
#### IPs

* **Dev:** 54.149.66.159
* **Production1:** 52.25.160.219
* **Production2:** 52.26.89.219
* **Dev Database:** 52.24.79.91
* **Emerald Server 1:** 10.0.0.101 (upstairs)
* **Emerald Server 1:** 10.0.0.103 (lab)

---
## Mathematica

##### Protocol Assignment:
```mathematica
Search[protocol[HPLC], Status == Requested];
ChangeProtocolStatus[protocol[748, HPLC], Enqueued];
Inform[person[57, Emerald] -> {CurrentProtocol -> protocol[748, HPLC]}];
```
##### Database Configuration:
```mathematica
Configuration["Connections", "SLL"]
```

##### Instrument Availability:
```mathematica
Search[instrument[HPLC], Status == Available];
Map[Inform[# -> {Status -> Available}] &, Search[instrument[HPLC], Status == Running]];
```

##### Reset Protocol to Movement:
```mathematica
ChangeProtocolStatus[protocol[752, HPLC], Troubleshooting];
ResetToTask[protocol[752, HPLC], "d08619b0-6ebb-4aca-b823-f2ba30daefbf"];
ResumeProtocol[protocol[752, HPLC]];
Inform[protocol[752, HPLC] -> {CurrentOperator -> $PersonID}]
```
---

## Rosetta Development

##### Create Recording:
```javascript
Backbone.Events.trigger("recorder:dump","/Users/erikmellum/Desktop/iolink-recordings/")
```
##### Replay Recording:
```bash
env IOLINK_RECORDING=~/Desktop/iolink-recordings/.json npm start
```
##### Mocking Recordings:
```javascript
pc.iolink.lookup._expressions
```

##### Launching:
```bash
cd ~/ecl/vagrant
vagrant ssh
devrun exec ecl/cmd/protoexec
cd ~/EmeraldSci/desktop/nw
node select-profile protoexec-dev
npm start
```
## ISE

##### Launching:

```bash
cd ~/ecl/vagrant
vagrant ssh
devrun exec ecl/cmd/cloudlab
cd ~/EmeraldSci/desktop/nw
node select-profile cloudlab-dev
npm start
```

## Object Store

```bash
ecldbinit createuser username:=erik email:=erik@e.com org_id:=1 password=e
```
