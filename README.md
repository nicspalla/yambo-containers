# yambo-containers
Recipes files for yambo containers.

An alternative to get the Yambo code is to install the Yambo container in your machine and this can be done in few steps:

## Install and configure Docker
Install the docker platform (Linux or Mac) following the instruction in the [docker website](https://docs.docker.com/engine/install/).

It is possible to run Docker by a normal user without the sudo privileges. In order to do that you have to add your username to the group "docker" (suggested on Linux!).

For Linux users:
```
sudo groupadd docker
sudo usermod -aG docker $USER
```

For Mac users:
```
sudo dscl . create /Groups/docker
sudo dseditgroup -o edit -a $USER -t user docker
```

Log out and log back in so that your group membership is re-evaluated.

If you prefer to use sudo please remember to add the "sudo" command before all the commands below.

## Prerequisites
Download the script file [`drun`](https://raw.githubusercontent.com/nicspalla/yambo-containers/main/drun) that will help you hiding the many options needed by the container:

```
wget https://raw.githubusercontent.com/nicspalla/yambo-containers/main/drun
```
then give the file execute privileges:
```
chmod +x drun
```

Move (or copy) this file in the directory where you want to use Yambo and use it as prefix of your Yambo calculation.

## Inizialization
First you have to initialize the environment needed by the container:
```
./drun -i
```
this command will pull the container if not already done and will create a file named env.txt needed by the container to run Yambo.

## Run
Now you can run yambo like in this example:
```
./drun yambo -F yambo.in -J yambo.out
```

These are the options of the script drun:
```
-i                 # container initialization
-np N              # Number of MPI tasks for a parallel run (default 0, i.e. serial run)
-t N               # Number of threads per process/task (default 1)
--env-file FILE    # set the path of an environment file (default ./env.txt)
-c IMAGE:TAG       # set the name and tag of the container image (default maxcentre/yambo:5.1.1_gcc9)
```

If the yambo container is working correctly this command
```
./drun yambo -h
```
should provide in output the help for yambo usage.

## Other
To delete the container images downloaded you can use this command:
```
docker image rm <image_name>
```

To remove all the stopped containers use this command:
```
docker system prune
```
