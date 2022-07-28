# Dockers
PS C:\Users\DELL> docker image pull alpine
Using default tag: latest
latest: Pulling from library/alpine
530afca65e2e: Pull complete
Digest: sha256:7580ece7963bfa863801466c0a488f11c86f85d9988051a9f9c68cb27f6b7872
Status: Downloaded newer image for alpine:latest
docker.io/library/alpine:latest
PS C:\Users\DELL> docker container run -it -v ilkvolume:/Deneme
"docker container run" requires at least 1 argument.
See 'docker container run --help'.

Usage:  docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]

Run a command in a new container
PS C:\Users\DELL> docker volume create ilkvolume
ilkvolume
PS C:\Users\DELL> docker inspect ilkvolume
[
    {
        "CreatedAt": "2022-07-28T22:35:53Z",
        "Driver": "local",
        "Labels": {},
        "Mountpoint": "/var/lib/docker/volumes/ilkvolume/_data",
        "Name": "ilkvolume",
        "Options": {},
        "Scope": "local"
    }
]
PS C:\Users\DELL> docker container run -it -v ilkvolume:/Deneme alpine sh
/ # ls
Deneme  dev     home    media   opt     root    sbin    sys     usr
bin     etc     lib     mnt     proc    run     srv     tmp     var
/ # cd/Deneme
sh: cd/Deneme: not found
/ # cd /Deneme
/Deneme # touch abc.txt
/Deneme # ls
abc.txt
/Deneme # echo "bunu ben ilk containerdan ekledim">>abc.txt
/Deneme # cat abc.txt
bunu ben ilk containerdan ekledim
/Deneme #
