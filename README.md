# Mostra tots els contenidor que hi ha corrent

> ## Sintaxi
> ``` bash
> $ docker ps [OPTIONS]
> ```
> [docker ps](https://docs.docker.com/engine/reference/commandline/ps/)


``` bash
docker ps
```

``` bash
CONTAINER ID   IMAGE                    COMMAND                  CREATED      STATUS      PORTS                               NAMES
3dc3f49b7582   docker/getting-started   "/docker-entrypoint.…"   3 days ago   Up 3 days   0.0.0.0:80->80/tcp, :::80->80/tcp   kind_goldberg
```

# Mostra tots els contenidor que hi ha corrent o aturats

``` bash
docker ps -a
```

``` bash
CONTAINER ID   IMAGE                    COMMAND                  CREATED      STATUS                     PORTS                               NAMES
3dc3f49b7582   docker/getting-started   "/docker-entrypoint.…"   3 days ago   Up 3 days ago              0.0.0.0:80->80/tcp, :::80->80/tcp   kind_goldberg
3de313ac6cf8   docker/getting-started   "/docker-entrypoint.…"   3 days ago   Exited (127) 3 days ago                                        infallible_ptolemy
c1ec48a5d129   hello-world              "/hello"                 3 days ago   Exited (0) 3 days ago                                          festive_elgamal
```

# Comanda per aturar contenidors

> ## Sintaxi
> ``` bash
> $ docker stop [OPTIONS] CONTAINER [CONTAINER...]
> ```
> [docker stop](https://docs.docker.com/engine/reference/commandline/stop/)


``` bash
sudo docker stop 3dc3f49b7582   
3dc3f49b7582

docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```


# Comanda per esborrar contenidors

> ## Sintaxi
> ``` bash
> $ docker rm [OPTIONS] CONTAINER [CONTAINER...]
> ```
> [docker rm](https://docs.docker.com/engine/reference/commandline/rm/)

``` bash
docker rm infallible_ptolemy
infallible_ptolemy

docker rm kind_goldberg
kind_goldberg

docker rm c1ec48a5d129
c1ec48a5d129

docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

# Comanda per crear un contenidor amb un nom concret (ourApp-<cognomAlumne>)

> ## Sintaxi
> ``` bash
> $ docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
> 
> ```
> [docker run](https://docs.docker.com/engine/reference/commandline/run/)


```bash
docker run --name ourApp-pardo  -d -p 80:80 docker/getting-started
36107d8aaa1cb9c63851082e20a2d4282474379d9eb9cca749b2b3038e42f033

docker ps -a
CONTAINER ID   IMAGE                    COMMAND                  CREATED              STATUS                          PORTS                               NAMES
36107d8aaa1c   docker/getting-started   "/docker-entrypoint.…"   5 seconds ago        Up 2 seconds                    0.0.0.0:80->80/tcp, :::80->80/tcp   ourApp-pardo
```

# Comanda per executar comandes dins d'un contenidor
> ## Sintaxi
> ``` bash
> $ docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
> 
> ```
> [docker exec](https://docs.docker.com/engine/reference/commandline/exec/)

```bash

```



``` bash
 wget https://github.com/docker/getting-started/archive/refs/heads/master.zip
--2022-10-10 07:14:07--  https://github.com/docker/getting-started/archive/refs/heads/master.zip
Resolving github.com (github.com)... 140.82.121.3
Connecting to github.com (github.com)|140.82.121.3|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://codeload.github.com/docker/getting-started/zip/refs/heads/master [following]
--2022-10-10 07:14:08--  https://codeload.github.com/docker/getting-started/zip/refs/heads/master
Resolving codeload.github.com (codeload.github.com)... 140.82.121.9
Connecting to codeload.github.com (codeload.github.com)|140.82.121.9|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 3083710 (2.9M) [application/zip]
Saving to: ‘master.zip’

master.zip                100%[===================================>]   2.94M  1.46MB/s    in 2.0s    

2022-10-10 07:14:10 (1.46 MB/s) - ‘master.zip’ saved [3083710/3083710]
```

