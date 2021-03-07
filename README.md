# gnbsim

gnbsim is a 5G SA gNB/UE simulator for testing 5G System.

This project is fork of `https://github.com/hhorai/gnbsim`.
It contains gnbsim tests for oai-5gcn.

## Build gnbsim docker image
```bash
docker build --tag gnbsim:latest --file docker/Dockerfile .
```
## Configure gnbsim

Edit test configuration in /example/example.json

## Build oai-cn5g docker images

Refer this page -> [oai-cn5g-fed](https://gitlab.eurecom.fr/oai/cn5g/oai-cn5g-fed/-/blob/master/docs/BUILD_IMAGES.md)

## Deploy oai-cn5g docker

Refer this page -> oai-cn5g-fed <br/>
or <br/>
Refer [sample docker-compose.](https://gitlab.eurecom.fr/kharade/gnbsim/-/blob/master/docker/docker-compose.yaml)
* `docker-compose up -d mysql`
* `docker-compose up vpp-upf`
* `docker-compose up oai-smf`
* `docker-compose up oai-amf`

## Run gnbsim

```bash
$ cd example
$ ./example
```

## Current status 
### Procedure tested
* gNB registration  
   -  NGSetup_Req/Resp
* UE registration
   -  NAS Auth req/resp IA_2
   -  Initial context setup req/resp
   -  UL NAS registration complete
* PDU session
   -  PDU session extablishment request
   -  PFCP session extablishment req/resp
   -  PDU session resource setup req + PDU session extablishment accept  
   -  PDU session resource setup resp
   -  PFCP session modification req/resp
   -  GTP UL/DL flow
### Procedure pending
   -  PDU session release

## Troubleshoot
* Remove tunnel interface <br/>
`ip tuntap del mode tun gtp-gnb`

* Log files and [setup diagram](https://gitlab.eurecom.fr/kharade/gnbsim/-/blob/master/logs/gnbsim_oai_5gcn.png) are [located here.](https://gitlab.eurecom.fr/kharade/gnbsim/-/tree/master/logs)
