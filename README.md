# Docker
Docker notes and samples

Docker is a very popular software container system. Unlikely Virtual Machines, docker instances are generally very light weight and are focused on a single process. 

# Docker commands

docker run hello-world

docker run -it ubuntu

docker run -ti ubuntu bash

docker image <cmd>

docker image ls

docker ps 

docker ps -l

docker images

docker commit <name> new_image_name

docker tag 18338f8s8af-hash new_image_name

docker run --rm -ti ubuntu sleep 5

docker run --rm -ti ubuntu bash -c "sleep 3;echo all done"

docker attach <name>

docker logs <name>

docker kill <name>

docker rm <name>

docker run --memory <max-allowed> <image-name> command

docker run --cpu-shares <percent>

docker port <name>

docker run --rm -ti -p 45678:45678 -p 45679:45679 --name my_doc_server ubuntu bash

nc -lp 45678 | nc -lp 45679

docker network <cmd>

docker network ls

docker network create

docker run -ti --rm --net=host ubuntu:18.04 bash

docker run -ti --rm --name my_docker ubuntu bash

docker inspect --format '{{.State.Pid}}' my_docker

docker pull

docker login

docker push

docker rmi # remove image

docker search node

docker run -ti -v /Users/dkruger/example:/shared-folder ubuntu bash  #shares a folder between host and docker and does the mapping

docker build -t <name-of-result> <path-to-docker-file>    # create an image

docker run -ti --volumes-from <name> ubuntu bash


# If running on Mac

1. use a subdirectory as /Users/blah directory has issues with .Trash

2. export the following variables

export DOCKER_BUILDKIT=0

export COMPOSE_DOCKER_CLI_BUILD=0

# Sample docker build
cat Dockerfile 

FROM ubuntu:20.04 as builder

RUN apt-get update

RUN apt-get -y install curl

RUN curl https://google.com | wc -c >google-size


FROM alpine

COPY --from=builder /google-size /google-size

ENTRYPOINT echo google is this big; cat google-size


# Build a docker image
docker build -t test .

Sending build context to Docker daemon  2.048kB

Step 1/7 : FROM ubuntu:20.04 as builder

20.04: Pulling from library/ubuntu

c549ccf8d472: Pull complete 

Digest: sha256:aba80b77e27148d99c034a987e7da3a287ed455390352663418c0f2ed40417fe

Status: Downloaded newer image for ubuntu:20.04

 ---> 9873176a8ff5

Step 2/7 : RUN apt-get update

 ---> Running in b4e4ba3e87dc

Get:1 http://security.ubuntu.com/ubuntu focal-security InRelease [114 kB]

Get:2 http://archive.ubuntu.com/ubuntu focal InRelease [265 kB]

Get:3 http://security.ubuntu.com/ubuntu focal-security/multiverse amd64 Packages [27.6 kB]

Get:4 http://security.ubuntu.com/ubuntu focal-security/main amd64 Packages [930 kB]

Get:5 http://archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]

Get:6 http://archive.ubuntu.com/ubuntu focal-backports InRelease [101 kB]

Get:7 http://security.ubuntu.com/ubuntu focal-security/universe amd64 Packages [779 kB]

Get:8 http://archive.ubuntu.com/ubuntu focal/universe amd64 Packages [11.3 MB]

Get:9 http://security.ubuntu.com/ubuntu focal-security/restricted amd64 Packages [368 kB]

Get:10 http://archive.ubuntu.com/ubuntu focal/multiverse amd64 Packages [177 kB]

Get:11 http://archive.ubuntu.com/ubuntu focal/main amd64 Packages [1275 kB]

Get:12 http://archive.ubuntu.com/ubuntu focal/restricted amd64 Packages [33.4 kB]

Get:13 http://archive.ubuntu.com/ubuntu focal-updates/multiverse amd64 Packages [32.0 kB]

Get:14 http://archive.ubuntu.com/ubuntu focal-updates/restricted amd64 Packages [416 kB]

Get:15 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [1367 kB]

Get:16 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [1051 kB]

Get:17 http://archive.ubuntu.com/ubuntu focal-backports/main amd64 Packages [2668 B]

Get:18 http://archive.ubuntu.com/ubuntu focal-backports/universe amd64 Packages [6303 B]

Fetched 18.4 MB in 20s (909 kB/s)

Reading package lists...

Removing intermediate container b4e4ba3e87dc

 ---> e4deae231057

Step 3/7 : RUN apt-get -y install curl

 ---> Running in 1fd7359e97f0

Reading package lists...

Building dependency tree...

Reading state information...

The following additional packages will be installed:

  ca-certificates krb5-locales libasn1-8-heimdal libbrotli1 libcurl4

  libgssapi-krb5-2 libgssapi3-heimdal libhcrypto4-heimdal libheimbase1-heimdal

  libheimntlm0-heimdal libhx509-5-heimdal libk5crypto3 libkeyutils1

  libkrb5-26-heimdal libkrb5-3 libkrb5support0 libldap-2.4-2 libldap-common

  libnghttp2-14 libpsl5 libroken18-heimdal librtmp1 libsasl2-2

  libsasl2-modules libsasl2-modules-db libsqlite3-0 libssh-4 libssl1.1

  libwind0-heimdal openssl publicsuffix

Suggested packages:

  krb5-doc krb5-user libsasl2-modules-gssapi-mit

  | libsasl2-modules-gssapi-heimdal libsasl2-modules-ldap libsasl2-modules-otp

  libsasl2-modules-sql

The following NEW packages will be installed:

  ca-certificates curl krb5-locales libasn1-8-heimdal libbrotli1 libcurl4

  libgssapi-krb5-2 libgssapi3-heimdal libhcrypto4-heimdal libheimbase1-heimdal

  libheimntlm0-heimdal libhx509-5-heimdal libk5crypto3 libkeyutils1

  libkrb5-26-heimdal libkrb5-3 libkrb5support0 libldap-2.4-2 libldap-common

  libnghttp2-14 libpsl5 libroken18-heimdal librtmp1 libsasl2-2

  libsasl2-modules libsasl2-modules-db libsqlite3-0 libssh-4 libssl1.1

  libwind0-heimdal openssl publicsuffix

0 upgraded, 32 newly installed, 0 to remove and 11 not upgraded.

Need to get 5445 kB of archives.

After this operation, 16.7 MB of additional disk space will be used.

Get:1 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libssl1.1 amd64 1.1.1f-1ubuntu2.4 [1319 kB]

Get:2 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 openssl amd64 1.1.1f-1ubuntu2.4 [620 kB]

Get:3 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 ca-certificates all 20210119~20.04.1 [146 kB]

Get:4 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libsqlite3-0 amd64 3.31.1-4ubuntu0.2 [549 kB]

Get:5 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 krb5-locales all 1.17-6ubuntu4.1 [11.4 kB]

Get:6 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libkrb5support0 amd64 1.17-6ubuntu4.1 [30.9 kB]

Get:7 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libk5crypto3 amd64 1.17-6ubuntu4.1 [79.9 kB]

Get:8 http://archive.ubuntu.com/ubuntu focal/main amd64 libkeyutils1 amd64 1.6-6ubuntu1 [10.2 kB]

Get:9 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libkrb5-3 amd64 1.17-6ubuntu4.1 [330 kB]

Get:10 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libgssapi-krb5-2 amd64 1.17-6ubuntu4.1 [121 kB]

Get:11 http://archive.ubuntu.com/ubuntu focal/main amd64 libpsl5 amd64 0.21.0-1ubuntu1 [51.5 kB]

Get:12 http://archive.ubuntu.com/ubuntu focal/main amd64 publicsuffix all 20200303.0012-1 [111 kB]

Get:13 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libbrotli1 amd64 1.0.7-6ubuntu0.1 [267 kB]

Get:14 http://archive.ubuntu.com/ubuntu focal/main amd64 libroken18-heimdal amd64 7.7.0+dfsg-1ubuntu1 [41.8 kB]

Get:15 http://archive.ubuntu.com/ubuntu focal/main amd64 libasn1-8-heimdal amd64 7.7.0+dfsg-1ubuntu1 [181 kB]

Get:16 http://archive.ubuntu.com/ubuntu focal/main amd64 libheimbase1-heimdal amd64 7.7.0+dfsg-1ubuntu1 [29.7 kB]

Get:17 http://archive.ubuntu.com/ubuntu focal/main amd64 libhcrypto4-heimdal amd64 7.7.0+dfsg-1ubuntu1 [87.9 kB]

Get:18 http://archive.ubuntu.com/ubuntu focal/main amd64 libwind0-heimdal amd64 7.7.0+dfsg-1ubuntu1 [48.0 kB]

Get:19 http://archive.ubuntu.com/ubuntu focal/main amd64 libhx509-5-heimdal amd64 7.7.0+dfsg-1ubuntu1 [107 kB]

Get:20 http://archive.ubuntu.com/ubuntu focal/main amd64 libkrb5-26-heimdal amd64 7.7.0+dfsg-1ubuntu1 [208 kB]

Get:21 http://archive.ubuntu.com/ubuntu focal/main amd64 libheimntlm0-heimdal amd64 7.7.0+dfsg-1ubuntu1 [15.1 kB]

Get:22 http://archive.ubuntu.com/ubuntu focal/main amd64 libgssapi3-heimdal amd64 7.7.0+dfsg-1ubuntu1 [96.1 kB]

Get:23 http://archive.ubuntu.com/ubuntu focal/main amd64 libsasl2-modules-db amd64 2.1.27+dfsg-2 [14.9 kB]

Get:24 http://archive.ubuntu.com/ubuntu focal/main amd64 libsasl2-2 amd64 2.1.27+dfsg-2 [49.3 kB]

Get:25 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libldap-common all 2.4.49+dfsg-2ubuntu1.8 [16.6 kB]

Get:26 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libldap-2.4-2 amd64 2.4.49+dfsg-2ubuntu1.8 [155 kB]

Get:27 http://archive.ubuntu.com/ubuntu focal/main amd64 libnghttp2-14 amd64 1.40.0-1build1 [78.7 kB]

Get:28 http://archive.ubuntu.com/ubuntu focal/main amd64 librtmp1 amd64 2.4+20151223.gitfa8646d.1-2build1 [54.9 kB]

Get:29 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libssh-4 amd64 0.9.3-2ubuntu2.1 [170 kB]

Get:30 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libcurl4 amd64 7.68.0-1ubuntu2.5 [234 kB]

Get:31 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 curl amd64 7.68.0-1ubuntu2.5 [161 kB]

Get:32 http://archive.ubuntu.com/ubuntu focal/main amd64 libsasl2-modules amd64 2.1.27+dfsg-2 [49.1 kB]

debconf: delaying package configuration, since apt-utils is not installed

Fetched 5445 kB in 7s (775 kB/s)

Selecting previously unselected package libssl1.1:amd64.

(Reading database ... 4127 files and directories currently installed.)

Preparing to unpack .../00-libssl1.1_1.1.1f-1ubuntu2.4_amd64.deb ...

Unpacking libssl1.1:amd64 (1.1.1f-1ubuntu2.4) ...

Selecting previously unselected package openssl.

Preparing to unpack .../01-openssl_1.1.1f-1ubuntu2.4_amd64.deb ...

Unpacking openssl (1.1.1f-1ubuntu2.4) ...

Selecting previously unselected package ca-certificates.

Preparing to unpack .../02-ca-certificates_20210119~20.04.1_all.deb ...

Unpacking ca-certificates (20210119~20.04.1) ...

Selecting previously unselected package libsqlite3-0:amd64.

Preparing to unpack .../03-libsqlite3-0_3.31.1-4ubuntu0.2_amd64.deb ...

Unpacking libsqlite3-0:amd64 (3.31.1-4ubuntu0.2) ...

Selecting previously unselected package krb5-locales.

Preparing to unpack .../04-krb5-locales_1.17-6ubuntu4.1_all.deb ...

Unpacking krb5-locales (1.17-6ubuntu4.1) ...

Selecting previously unselected package libkrb5support0:amd64.

Preparing to unpack .../05-libkrb5support0_1.17-6ubuntu4.1_amd64.deb ...

Unpacking libkrb5support0:amd64 (1.17-6ubuntu4.1) ...

Selecting previously unselected package libk5crypto3:amd64.

Preparing to unpack .../06-libk5crypto3_1.17-6ubuntu4.1_amd64.deb ...

Unpacking libk5crypto3:amd64 (1.17-6ubuntu4.1) ...

Selecting previously unselected package libkeyutils1:amd64.

Preparing to unpack .../07-libkeyutils1_1.6-6ubuntu1_amd64.deb ...

Unpacking libkeyutils1:amd64 (1.6-6ubuntu1) ...

Selecting previously unselected package libkrb5-3:amd64.

Preparing to unpack .../08-libkrb5-3_1.17-6ubuntu4.1_amd64.deb ...

Unpacking libkrb5-3:amd64 (1.17-6ubuntu4.1) ...

Selecting previously unselected package libgssapi-krb5-2:amd64.

Preparing to unpack .../09-libgssapi-krb5-2_1.17-6ubuntu4.1_amd64.deb ...

Unpacking libgssapi-krb5-2:amd64 (1.17-6ubuntu4.1) ...

Selecting previously unselected package libpsl5:amd64.

Preparing to unpack .../10-libpsl5_0.21.0-1ubuntu1_amd64.deb ...

Unpacking libpsl5:amd64 (0.21.0-1ubuntu1) ...

Selecting previously unselected package publicsuffix.

Preparing to unpack .../11-publicsuffix_20200303.0012-1_all.deb ...

Unpacking publicsuffix (20200303.0012-1) ...

Selecting previously unselected package libbrotli1:amd64.

Preparing to unpack .../12-libbrotli1_1.0.7-6ubuntu0.1_amd64.deb ...

Unpacking libbrotli1:amd64 (1.0.7-6ubuntu0.1) ...

Selecting previously unselected package libroken18-heimdal:amd64.

Preparing to unpack .../13-libroken18-heimdal_7.7.0+dfsg-1ubuntu1_amd64.deb ...

Unpacking libroken18-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Selecting previously unselected package libasn1-8-heimdal:amd64.

Preparing to unpack .../14-libasn1-8-heimdal_7.7.0+dfsg-1ubuntu1_amd64.deb ...

Unpacking libasn1-8-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Selecting previously unselected package libheimbase1-heimdal:amd64.

Preparing to unpack .../15-libheimbase1-heimdal_7.7.0+dfsg-1ubuntu1_amd64.deb ...

Unpacking libheimbase1-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Selecting previously unselected package libhcrypto4-heimdal:amd64.

Preparing to unpack .../16-libhcrypto4-heimdal_7.7.0+dfsg-1ubuntu1_amd64.deb ...

Unpacking libhcrypto4-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Selecting previously unselected package libwind0-heimdal:amd64.

Preparing to unpack .../17-libwind0-heimdal_7.7.0+dfsg-1ubuntu1_amd64.deb ...

Unpacking libwind0-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Selecting previously unselected package libhx509-5-heimdal:amd64.

Preparing to unpack .../18-libhx509-5-heimdal_7.7.0+dfsg-1ubuntu1_amd64.deb ...

Unpacking libhx509-5-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Selecting previously unselected package libkrb5-26-heimdal:amd64.

Preparing to unpack .../19-libkrb5-26-heimdal_7.7.0+dfsg-1ubuntu1_amd64.deb ...

Unpacking libkrb5-26-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Selecting previously unselected package libheimntlm0-heimdal:amd64.

Preparing to unpack .../20-libheimntlm0-heimdal_7.7.0+dfsg-1ubuntu1_amd64.deb ...

Unpacking libheimntlm0-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Selecting previously unselected package libgssapi3-heimdal:amd64.

Preparing to unpack .../21-libgssapi3-heimdal_7.7.0+dfsg-1ubuntu1_amd64.deb ...

Unpacking libgssapi3-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Selecting previously unselected package libsasl2-modules-db:amd64.

Preparing to unpack .../22-libsasl2-modules-db_2.1.27+dfsg-2_amd64.deb ...

Unpacking libsasl2-modules-db:amd64 (2.1.27+dfsg-2) ...

Selecting previously unselected package libsasl2-2:amd64.

Preparing to unpack .../23-libsasl2-2_2.1.27+dfsg-2_amd64.deb ...

Unpacking libsasl2-2:amd64 (2.1.27+dfsg-2) ...

Selecting previously unselected package libldap-common.

Preparing to unpack .../24-libldap-common_2.4.49+dfsg-2ubuntu1.8_all.deb ...

Unpacking libldap-common (2.4.49+dfsg-2ubuntu1.8) ...

Selecting previously unselected package libldap-2.4-2:amd64.

Preparing to unpack .../25-libldap-2.4-2_2.4.49+dfsg-2ubuntu1.8_amd64.deb ...

Unpacking libldap-2.4-2:amd64 (2.4.49+dfsg-2ubuntu1.8) ...

Selecting previously unselected package libnghttp2-14:amd64.

Preparing to unpack .../26-libnghttp2-14_1.40.0-1build1_amd64.deb ...

Unpacking libnghttp2-14:amd64 (1.40.0-1build1) ...

Selecting previously unselected package librtmp1:amd64.

Preparing to unpack .../27-librtmp1_2.4+20151223.gitfa8646d.1-2build1_amd64.deb ...

Unpacking librtmp1:amd64 (2.4+20151223.gitfa8646d.1-2build1) ...

Selecting previously unselected package libssh-4:amd64.

Preparing to unpack .../28-libssh-4_0.9.3-2ubuntu2.1_amd64.deb ...

Unpacking libssh-4:amd64 (0.9.3-2ubuntu2.1) ...

Selecting previously unselected package libcurl4:amd64.

Preparing to unpack .../29-libcurl4_7.68.0-1ubuntu2.5_amd64.deb ...

Unpacking libcurl4:amd64 (7.68.0-1ubuntu2.5) ...

Selecting previously unselected package curl.

Preparing to unpack .../30-curl_7.68.0-1ubuntu2.5_amd64.deb ...

Unpacking curl (7.68.0-1ubuntu2.5) ...

Selecting previously unselected package libsasl2-modules:amd64.

Preparing to unpack .../31-libsasl2-modules_2.1.27+dfsg-2_amd64.deb ...

Unpacking libsasl2-modules:amd64 (2.1.27+dfsg-2) ...

Setting up libkeyutils1:amd64 (1.6-6ubuntu1) ...

Setting up libpsl5:amd64 (0.21.0-1ubuntu1) ...

Setting up libssl1.1:amd64 (1.1.1f-1ubuntu2.4) ...

debconf: unable to initialize frontend: Dialog

debconf: (TERM is not set, so the dialog frontend is not usable.)

debconf: falling back to frontend: Readline

debconf: unable to initialize frontend: Readline

debconf: (Can't locate Term/ReadLine.pm in @INC (you may need to install the Term::ReadLine module) (@INC contains: /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.30.0 /usr/local/share/perl/5.30.0 /usr/lib/x86_64-linux-gnu/perl5/5.30 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl/5.30 /usr/share/perl/5.30 /usr/local/lib/site_perl /usr/lib/x86_64-linux-gnu/perl-base) at /usr/share/perl5/Debconf/FrontEnd/Readline.pm line 7.)

debconf: falling back to frontend: Teletype

Setting up libbrotli1:amd64 (1.0.7-6ubuntu0.1) ...

Setting up libsqlite3-0:amd64 (3.31.1-4ubuntu0.2) ...

Setting up libsasl2-modules:amd64 (2.1.27+dfsg-2) ...

Setting up libnghttp2-14:amd64 (1.40.0-1build1) ...

Setting up krb5-locales (1.17-6ubuntu4.1) ...

Setting up libldap-common (2.4.49+dfsg-2ubuntu1.8) ...

Setting up libkrb5support0:amd64 (1.17-6ubuntu4.1) ...

Setting up libsasl2-modules-db:amd64 (2.1.27+dfsg-2) ...

Setting up librtmp1:amd64 (2.4+20151223.gitfa8646d.1-2build1) ...

Setting up libk5crypto3:amd64 (1.17-6ubuntu4.1) ...

Setting up libsasl2-2:amd64 (2.1.27+dfsg-2) ...

Setting up libroken18-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Setting up libkrb5-3:amd64 (1.17-6ubuntu4.1) ...

Setting up openssl (1.1.1f-1ubuntu2.4) ...

Setting up publicsuffix (20200303.0012-1) ...

Setting up libheimbase1-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Setting up libasn1-8-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Setting up libhcrypto4-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Setting up ca-certificates (20210119~20.04.1) ...

debconf: unable to initialize frontend: Dialog

debconf: (TERM is not set, so the dialog frontend is not usable.)

debconf: falling back to frontend: Readline

debconf: unable to initialize frontend: Readline

debconf: (Can't locate Term/ReadLine.pm in @INC (you may need to install the Term::ReadLine module) (@INC contains: /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.30.0 /usr/local/share/perl/5.30.0 /usr/lib/x86_64-linux-gnu/perl5/5.30 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl/5.30 /usr/share/perl/5.30 /usr/local/lib/site_perl /usr/lib/x86_64-linux-gnu/perl-base) at /usr/share/perl5/Debconf/FrontEnd/Readline.pm line 7.)

debconf: falling back to frontend: Teletype

Updating certificates in /etc/ssl/certs...

129 added, 0 removed; done.

Setting up libwind0-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Setting up libgssapi-krb5-2:amd64 (1.17-6ubuntu4.1) ...

Setting up libssh-4:amd64 (0.9.3-2ubuntu2.1) ...

Setting up libhx509-5-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Setting up libkrb5-26-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Setting up libheimntlm0-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Setting up libgssapi3-heimdal:amd64 (7.7.0+dfsg-1ubuntu1) ...

Setting up libldap-2.4-2:amd64 (2.4.49+dfsg-2ubuntu1.8) ...

Setting up libcurl4:amd64 (7.68.0-1ubuntu2.5) ...

Setting up curl (7.68.0-1ubuntu2.5) ...

Processing triggers for libc-bin (2.31-0ubuntu9.2) ...

Processing triggers for ca-certificates (20210119~20.04.1) ...

Updating certificates in /etc/ssl/certs...

0 added, 0 removed; done.

Running hooks in /etc/ca-certificates/update.d...

done.

Removing intermediate container 1fd7359e97f0

 ---> 7dc03594ddc9

Step 4/7 : RUN curl https://google.com | wc -c >google-size

 ---> Running in 42ca85f5f79c

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current

                                 Dload  Upload   Total   Spent    Left  Speed

100   220  100   220    0     0    565      0 --:--:-- --:--:-- --:--:--   564

Removing intermediate container 42ca85f5f79c

 ---> 87e7a82eda3b

Step 5/7 : FROM alpine

latest: Pulling from library/alpine

5843afab3874: Pull complete 

Digest: sha256:234cb88d3020898631af0ccbbcca9a66ae7306ecd30c9720690858c1b007d2a0

Status: Downloaded newer image for alpine:latest

 ---> d4ff818577bc

Step 6/7 : COPY --from=builder /google-size /google-size

 ---> c33c0da41ba7

Step 7/7 : ENTRYPOINT echo google is this big; cat google-size

 ---> Running in 15beb386300e

Removing intermediate container 15beb386300e

 ---> 0d0ce700c034

Successfully built 0d0ce700c034

Successfully tagged test:latest



Use 'docker scan' to run Snyk tests against images to find vulnerabilities and learn how to fix them
