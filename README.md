#Apache Hadoop 2.7.1 Docker image

# Build the image

If you'd like to try directly from the Dockerfile you can build the image as:

```
sudo docker build -t hadoop/bonsai-master:2.7.1 .
```

# In order to start a hadoop master, 

Create a new subnet for the the cluster so that you can assign static ip addresses

```
sudo docker network create --subnet=172.18.0.0/16 bonsai-net

```

## You need to make sure that you start the worker nodes. 

The idea is to fork a minimum of 3 workers and there is nothing in following the instructions as is

```
sudo docker run -it -h bonsai-worker-1 --ip 172.18.0.5 --add-host bonsai-master:172.18.0.2 --add-host bonsai-worker-2:172.18.0.6 --add-host bonsai-worker-3:172.18.0.7 --net bonsai-net hadoop/bonsai-worker:2.7.1 /etc/bootstrap.sh -bash

sudo docker run -it -h bonsai-worker-2 --ip 172.18.0.6 --add-host bonsai-master:172.18.0.2 --add-host bonsai-worker-3:172.18.0.7 --add-host bonsai-worker-1:172.18.0.5 --net bonsai-net hadoop/bonsai-worker:2.7.1 /etc/bootstrap.sh -bash

sudo docker run -it -h bonsai-worker-3 --ip 172.18.0.7 --add-host bonsai-master:172.18.0.2 --add-host bonsai-worker-2:172.18.0.6 --add-host bonsai-worker-1:172.18.0.5 --net bonsai-net hadoop/bonsai-worker:2.7.1 /etc/bootstrap.sh -bash
```

