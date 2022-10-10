# Act-Our-App

## Mostra tots els contenidor que hi ha corrent

> ### ***Sintaxi***
``` bash
> docker ps [OPTIONS]
> ```
> [més info. a **docker ps** (docs.docker.com)](https://docs.docker.com/engine/reference/commandline/ps/)
> <br>
<br>


``` bash
$ docker ps

CONTAINER ID   IMAGE                    COMMAND                  CREATED      STATUS      PORTS                               NAMES
3dc3f49b7582   docker/getting-started   "/docker-entrypoint.…"   3 days ago   Up 3 days   0.0.0.0:80->80/tcp, :::80->80/tcp   kind_goldberg
```

## Mostra tots els contenidor que hi ha corrent o aturats

``` bash
$ docker ps -a
```

``` bash
CONTAINER ID   IMAGE                    COMMAND                  CREATED      STATUS                     PORTS                               NAMES
3dc3f49b7582   docker/getting-started   "/docker-entrypoint.…"   3 days ago   Up 3 days ago              0.0.0.0:80->80/tcp, :::80->80/tcp   kind_goldberg
3de313ac6cf8   docker/getting-started   "/docker-entrypoint.…"   3 days ago   Exited (127) 3 days ago                                        infallible_ptolemy
c1ec48a5d129   hello-world              "/hello"                 3 days ago   Exited (0) 3 days ago                                          festive_elgamal
```

## Comanda per aturar contenidors

> ### ***Sintaxi***
``` bash
> $ docker stop [OPTIONS] CONTAINER [CONTAINER...]
> ```
> [més info. a **docker stop** (docs.docker.com)](https://docs.docker.com/engine/reference/commandline/stop/)
> <br>
<br>


``` bash
$ docker stop 3dc3f49b7582   
3dc3f49b7582

$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```


## Comanda per esborrar contenidors

> ### ***Sintaxi***
``` bash
> $ docker rm [OPTIONS] CONTAINER [CONTAINER...]
> ```
> [més info. a **docker rm** (docs.docker.com)](https://docs.docker.com/engine/reference/commandline/rm/)
> <br>
<br>

``` bash
$ docker rm infallible_ptolemy
infallible_ptolemy

$ docker rm kind_goldberg
kind_goldberg

$ docker rm c1ec48a5d129
c1ec48a5d129

$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

## Comanda per crear un contenidor amb un nom concret (ourApp-<cognomAlumne>)

> ### ***Sintaxi***
``` bash
> $ docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
> 
> ```
> [més info. a **docker run** (docs.docker.com)](https://docs.docker.com/engine/reference/commandline/run/)
> <br>
<br>


```bash
$ docker run --name ourApp-pardo  -d -p 80:80 docker/getting-started
36107d8aaa1cb9c63851082e20a2d4282474379d9eb9cca749b2b3038e42f033

$ docker ps -a
CONTAINER ID   IMAGE                    COMMAND                  CREATED              STATUS                          PORTS                               NAMES
36107d8aaa1c   docker/getting-started   "/docker-entrypoint.…"   5 seconds ago        Up 2 seconds                    0.0.0.0:80->80/tcp, :::80->80/tcp   ourApp-pardo
```

## Comanda per executar comandes dins d'un contenidor

> ### ***Sintaxi***
``` bash
> $ docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
> 
> ```
> [més info. a **docker exec** (docs.docker.com)](https://docs.docker.com/engine/reference/commandline/exec/)
> <br>
<br>

```bash
$ docker exec -it ourApp-pardo sh
/ # 
```

Un cop que som dins de la consola del nostre contenidor, abans de continuar li cambiarem el ```prompt```.

```bash
$export PS1="\u@\h \w> "
root@36107d8aaa1c /> 
$
```

Així veiem quin és el nom de l'usuari, seguit del servidor i per últim el directori a on ens trobem.
Fixeu-vos que el nom del host, és el mateix que la part de l'identificador del contenidor, que es mostra quan se'ns llista la informació dels contenidors.

A continuació executem el següent per tancar la sessió del contenidor:
```bash
root@36107d8aaa1c /> exit
```

Fins aquí hem après diferents comandes de ```docker```. Ara passarem a crear un nou contenidor a on instal·larem una aplicació.

Un cop tornem a estar al nostre host, ens descarragarem el fitxer que ens baixarà la nostra aplicació.

Per fer-ho seguirem els següents pasos:

**1.** Crearem una carpeta amb el nom de ```<cognomAlumne>-our-app``` i ens col·locarem a l'interior.

``` bash
 ~$ cd <cognomAlumne>-our-app
 ~$ mkdir <cognomAlumne>-our-app
 ~$ cd <cognomAlumne>-our-app
 ~/<cognomAlumne>-our-app $ cd <cognomAlumne>-our-app
 ~/<cognomAlumne>-our-app $ wget https://github.com/docker/getting-started/archive/refs/heads/master.zip
 Connecting to github.com (140.82.121.4:443)
 Connecting to codeload.github.com (140.82.121.10:443)
 saving to 'master.zip'
 master.zip           100% |******************************************************| 3011k  0:00:00 ETA
 'master.zip' saved
 ~/<cognomAlumne>-our-app $  ls -l
total 3012
-rw-rw-r-- 1 joan joan 3083710 Oct 10 07:14 master.zip
```

**2.** A continucaió descomprimim el fitxer que ens hem descarregat.

```bash
~/<cognomAlumne>-our-app $ unzip master.zip 
Command 'unzip' not found, but can be installed with:
```

**2.b.** I si no tenim el programa ```unzip``` l'instal·lem.

```bash
sudo apt install unzip
~/<cognomAlumne>-our-app $ sudo apt install unzip
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Suggested packages:
  zip
The following NEW packages will be installed:
  unzip
0 upgraded, 1 newly installed, 0 to remove and 40 not upgraded.
Need to get 174 kB of archives.
After this operation, 385 kB of additional disk space will be used.
Get:1 http://es.archive.ubuntu.com/ubuntu jammy/main amd64 unzip amd64 6.0-26ubuntu3 [174 kB]
Fetched 174 kB in 1s (218 kB/s)
Selecting previously unselected package unzip.
(Reading database ... 73614 files and directories currently installed.)
Preparing to unpack .../unzip_6.0-26ubuntu3_amd64.deb ...
Unpacking unzip (6.0-26ubuntu3) ...
Setting up unzip (6.0-26ubuntu3) ...
Processing triggers for man-db (2.10.2-1) ...
Scanning processes...                                                                                 
Scanning linux images...                                                                              

Running kernel seems to be up-to-date.

No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.

No VM guests are running outdated hypervisor (qemu) binaries on this host.
~/<cognomAlumne>-our-app $
```

**3.** Ara sí el descomprimim i llistem el que tenim.

``` bash
 ~/<cognomAlumne>-our-app $ unzip master.zip
 Archive:  master.zip
    creating: getting-started-master/
   inflating: getting-started-master/.dockerignore
    creating: getting-started-master/.github/
 ...
   inflating: getting-started-master/mkdocs.yml
   inflating: getting-started-master/requirements.txt
   inflating: getting-started-master/yarn.lock
 ~/<cognomAlumne>-our-app $ ls -l
 total 3016
 drwxrwxrwx    5 root     root          4096 Oct 10 08:24 getting-started-master
 -rw-r--r--    1 root     root       3083710 Oct 10 08:19 master.zip
```

**4.** Entrem a la carpeta ```getting-started-master``` i llistem el seu contingut:
```bash
 ~/<cognomAlumne>-our-app>cd getting-started-master
 ~/<cognomAlumne>-our-app/getting-started-master> ls -l
 total 52
 -rw-r--r--    1 root     root          1078 Oct 10 08:24 Dockerfile
 -rw-r--r--    1 root     root           535 Oct 10 08:24 Jenkinsfile
 -rw-r--r--    1 root     root         11356 Oct 10 08:24 LICENSE
 -rw-r--r--    1 root     root          1668 Oct 10 08:24 README.md
 drwxrwxrwx    4 root     root          4096 Oct 10 08:24 app
 -rwxr-xr-x    1 root     root           253 Oct 10 08:24 build.sh
 -rw-r--r--    1 root     root           167 Oct 10 08:24 docker-compose.yml
 drwxrwxrwx    6 root     root          4096 Oct 10 08:24 docs
 -rw-r--r--    1 root     root          1990 Oct 10 08:24 mkdocs.yml
 -rw-r--r--    1 root     root           105 Oct 10 08:24 requirements.txt
 -rw-r--r--    1 root     root            86 Oct 10 08:24 yarn.lock
 
 ```

**5.** A continuació ens movem a la carpeta ```app```.

```bash
~/<cognomAlumne>-our-app/getting-started-master> cd app
~/<cognomAlumne>-our-app/getting-started-master/app $
```

**6.** Llistem el seu contigut i confirmem que hi ha un fitxer anomenat ```package.json``` en aquest fitxer guardem part de la configuració pel contenidor que anem a crear. I també trobem dues carpetes amb els noms ```spec``` i ```src``` que contenen el codi font de la nostra aplicació.

```bash
~/<cognomAlumne>-our-app/getting-started-master/app $ ls -l
total 184
-rw-rw-r-- 1 joan joan    646 Aug 30 12:55 package.json
drwxrwxr-x 4 joan joan   4096 Aug 30 12:55 spec
drwxrwxr-x 5 joan joan   4096 Aug 30 12:55 src
-rw-rw-r-- 1 joan joan 174891 Aug 30 12:55 yarn.lock
~/<cognomAlumne>-our-app/getting-started-master/app $ 
```


**7.** A la mateixa carpeta a on es troba el fitxer anomenat ```package.json```, és a dir dins de la carpeta anomenada ```app``` cal que creem el següent fitxer ```Dockerfile```. És **TAN** imporant a **on es troba** aquest fitxer, com **el nom**, ja que si el nom no és ```Dockerfile```, no funcionarà! Per crear el fitxer farem servir ```**vi**```.

```bash
~/<cognomAlumne>-our-app/getting-started-master/app $ vi Dockerfile
```

Un cop siguem dins de l'editor vi, el fitxer estarà buit.
```bash

 ~
 ~
 ~
 ...
 ~
 ~
 "Dockerfile" [New]                                                                  0,0-1         All
```

**8.** Ara pitjem la tecla **```i```** de **Insert**.
```bash
 
 ~
 ...
 ~
 ~
 -- INSERT --                                                                        0,1           All
```

Veiem com a la part inferior apareix la paruala ```**INSERT**```.

**6.** Ara cal copiar el següent text: 
```bash
# syntax=docker/dockerfile:1
FROM node:12-alpine
RUN apk add --no-cache python2 g++ make
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000
```

**7.** Un cop ja tenim el contingut del fitxer, llavors pitjem *```:wq```*, per guardar i tancar el document.

```bash
 # syntax=docker/dockerfile:1
 FROM node:12-alpine
 RUN apk add --no-cache python2 g++ make
 WORKDIR /app
 COPY . .
 RUN yarn install --production
 CMD ["node", "src/index.js"]
 EXPOSE 3000
 ~
 ...
 ~
 :wq                     
```


**8.** Confirmem que el fitxer existeix.

```bash
 ~/<cognomAlumne>-our-app/getting-started-master/app $ ls -l
 total 188
 -rw-rw-r-- 1 joan joan    182 Oct 10 09:10 Dockerfile
 -rw-rw-r-- 1 joan joan    646 Aug 30 12:55 package.json
 drwxrwxr-x 4 joan joan   4096 Aug 30 12:55 spec
 drwxrwxr-x 5 joan joan   4096 Aug 30 12:55 src
 -rw-rw-r-- 1 joan joan 174891 Aug 30 12:55 yarn.lock
 ~/<cognomAlumne>-our-app/getting-started-master/app $ 
```


**9.** Ara procedim a crear la imatge amb la comanda ```build```.

> ### ***Sintaxi***
> ``` bash
> $ docker build [OPTIONS] PATH | URL | 
> ```
> [més info. a **docker build** (docs.docker.com)](https://docs.docker.com/engine/reference/commandline/build/)
> <br>
<br>

Per crear la imatge executarem la següent comanda:


```bash
~/<cognomAlumne>-our-app/getting-started-master/app $ docker build -t getting-started .
Sending build context to Docker daemon  4.654MB
Step 1/7 : FROM node:12-alpine
12-alpine: Pulling from library/node
df9b9388f04a: Already exists 
3bf6d7380205: Pull complete 
7939e601ee5e: Pull complete 
31f0fb9de071: Pull complete 
Digest: sha256:d4b15b3d48f42059a15bd659be60afe21762aae9d6cbea6f124440895c27db68
Status: Downloaded newer image for node:12-alpine
 ---> bb6d28039b8c
Step 2/7 : RUN apk add --no-cache python2 g++ make
 ---> Running in f18b791a0bf8
fetch https://dl-cdn.alpinelinux.org/alpine/v3.15/main/x86_64/APKINDEX.tar.gz
fetch https://dl-cdn.alpinelinux.org/alpine/v3.15/community/x86_64/APKINDEX.tar.gz
...
Step 4/7 : COPY . .
 ---> d63abfb33bd1
Step 5/7 : RUN yarn install --production
 ---> Running in 23ffd93a4c9a
yarn install v1.22.18
[1/4] Resolving packages...
warning Resolution field "ansi-regex@5.0.1" is incompatible with requested version "ansi-regex@^2.0.0"
warning Resolution field "ansi-regex@5.0.1" is incompatible with requested version "ansi-regex@^3.0.0"
[2/4] Fetching packages...
[3/4] Linking dependencies...
[4/4] Building fresh packages...
Done in 23.76s.
Removing intermediate container 23ffd93a4c9a
 ---> dbd8db4db3e4
Step 6/7 : CMD ["node", "src/index.js"]
 ---> Running in ecc4009e82aa
Removing intermediate container ecc4009e82aa
 ---> aa3ee49cbbd0
Step 7/7 : EXPOSE 3000
 ---> Running in f25d41e30092
Removing intermediate container f25d41e30092
 ---> b779a17ac56f
Successfully built b779a17ac56f
Successfully tagged getting-started:latest
```

**10.** Iniciem el contenidor a partir de la imatge que acabem de crear.

```bash
 ~/<cognomAlumne>-our-app/getting-started-master/app $ sudo docker run --name pardoApp -dp 3000:3000 getting-started
6371851095efc8657b63e54f74010698ec20abc54be0ecfbcc794f62bdaf8e77
 ~/<cognomAlumne>-our-app/getting-started-master/app $ sudo docker ps
CONTAINER ID   IMAGE                    COMMAND                  CREATED          STATUS          PORTS                                       NAMES
6371851095ef   getting-started          "docker-entrypoint.s…"   19 seconds ago   Up 18 seconds   0.0.0.0:3000->3000/tcp, :::3000->3000/tcp   pardoApp
36107d8aaa1c   docker/getting-started   "/docker-entrypoint.…"   6 hours ago      Up 6 hours      0.0.0.0:80->80/tcp, :::80->80/tcp           ourApp-pardo
 ```

**X.**

>```bash
> ```

