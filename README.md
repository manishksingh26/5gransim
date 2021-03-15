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

Refer this page -> [oai-cn5g-fed](https://gitlab.eurecom.fr/oai/cn5g/oai-cn5g-fed/-/blob/master/docs/BUILD_IMAGES.md) for building AMF, SMF, UPF (develop branch).
Below test is done with [vpp-upf (Travelping)](https://gitlab.eurecom.fr/oai/cn5g/oai-cn5g-upf-vpp/-/blob/vpp-upf/docs/BUILD_IMAGE.md), AMF (develop branch) and SMF (vpp-upf branch)

## Deploy oai-cn5g docker

Refer this page -> [oai-cn5g-fed](https://gitlab.eurecom.fr/oai/cn5g/oai-cn5g-fed/-/blob/master/docs/BUILD_IMAGES.md) to deploy oai-cn5g components.<br/>
or <br/>
Refer oai-cn5g-fed [sample docker-compose.](https://gitlab.eurecom.fr/kharade/gnbsim/-/blob/master/docker/docker-compose.yaml)
`cd docker/ && docker-compose config --services` # To list docker services 
* `docker-compose up -d mysql`  (Configure IMSI as per instruction on [OAI-wiki for AMF](https://gitlab.eurecom.fr/oai/cn5g/oai-cn5g-amf/-/wikis/Installation))
* `docker-compose up -d vpp-upf` 
* `docker-compose up -d oai-smf`
* `docker-compose up -d oai-amf`
* `docker-compose up -d gnbsim`

##### Note :- gnbsim requires gtp kernel module (by default present in linux kernel 4.7.0 onward) to be mounted inside docker container.
##### Verify mount source for gtp kernel module by command <br/>
 `find /lib/modules/$(uname -r) -name gtp.ko`. <br/>
 Then update gtp kernel volume mount for service gnbsim in docker-compose.

## Run gnbsim

```bash
$ docker exec -it gnbsim bash
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
   -  GTP UL/DL flow (with/without gtp extension header)
* UE deregistration

### Procedure pending
   -  PDU session release

## Troubleshoot
* Remove tunnel interface <br/>
`ip tuntap del mode tun gtp-gnb`

* Log files and [setup diagram](https://gitlab.eurecom.fr/kharade/gnbsim/-/blob/master/logs/gnbsim_oai_5gcn.png) are [located here.](https://gitlab.eurecom.fr/kharade/gnbsim/-/tree/master/logs)
