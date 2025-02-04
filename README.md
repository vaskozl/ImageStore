# ImageStore

ImageStore is a self-hosted photo gallery, that makes Google Photos users feel right at home.

## Features:
- Clean and intuitive UI for desktop and mobile browsers
- Automatic thumbnail and preview creation for faster loading times
- Fast uploads for both photos and videos
- Albums to sort your photos into
- Easily searchable labels
- Automatic image-tagging

[Online demo](https://gregordr.github.io/ImageStore/)

This should give you a feeling of how everything works with some images of cats. Or, take a look below:

To upload your own images, you will of course need to self-host.

![preview](https://imgur.com/0yZQ7c7.jpg)

## Installation instructions:

### Docker prebuilt images

Requirements:

 - Docker
 - Docker-compose
 - For automatic labeling: x86_64 CPU (also known as x64, x86_64, AMD64 and Intel 64)

Download the docker-compose.yml: ```wget https://raw.githubusercontent.com/gregordr/ImageStore/main/docker-compose.yml```.

Edit it according to your liking, then run ```docker-compose up```. Note that you need to comment back in one of the two labelers, in case you want automatic image labeling.

Go to http://localhost:3000, or alternatively the port you have chosen to use.

### Docker build images yourself

Requirements:
 - Docker
 - Docker-compose
 - For automatic labeling: x86_64 CPU (also known as x64, x86_64, AMD64 and Intel 64)

If you want to build yourself, then clone this repo and run ```docker-compose -f docker-compose-build.yml up```

### Without docker
Requires Ubuntu 18.04/20.04. A RHEL/Centos build is in the works.

```
git clone https://github.com/gregordr/ImageStore
cd CLI-Install
sudo ./imagestore-build.sh
```
This will install and configure everything as needed in order to host ImageStore. PostgreSQL 11, Nodejs and nginx will be installed.
By default it hosts over port 8080. However, the script has built in error checking such that if you're already hosting something over that port, 
it will detect it and ask for an alternate port. The created database user is seeded with a random 16 character string, so there 
is no default password to worry about. 

The Imagestore service by default will start on boot. To stop Imagestore, run
```sudo systemctl stop ImageStoreFRONT.service; sudo systemctl stop ImageStoreBACK.service;```

To prevent the service from starting on boot, run 
```sudo systemctl disable ImageStoreFRONT.service; sudo systemctl disable ImageStoreBACK.service;```

### Notes for raspberry Pi:

Incase you get an error with the backend saying unreachable code, you might have to run the following commands:

```
wget http://ftp.ch.debian.org/debian/pool/main/libs/libseccomp/libseccomp2_2.5.1-1_armhf.deb
sha256sum libseccomp2_2.5.1-1_armhf.deb
# CONFIRM THAT THE OUTPUT MATCHES THE FOLLOWING LINE BEFORE YOU RUN THE LAST COMMAND:
# 7a4d09eea20f7e17a416825ae2be06ca08b9cb5072566045c545c74192e6fcca  libseccomp2_2.5.1-1_armhf.deb
sudo dpkg -i libseccomp2_2.5.1-1_armhf.deb
```

## Contributing:

Accepted feature requests can be seen under projects/ToDOs. If you have a new feature request, feel free to open an issue.

If you would like to implement a feature, please create a PR to the ```test``` branch.
