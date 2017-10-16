docker-machine create -d virtualbox node-1
docker-machine ssh node-1
uname -r
whoami
ps aux
ls /home
hostname
docker version
docker pull ubuntu
docker images ubuntu
docker run ubuntu echo "Hello World"
docker ps
docker ps -a
docker rm <ID>
docker run -it --rm ubuntu
uname -r
cat /etc/lsb-release
whoami
ls /home
ps aux
hostname
sleep 321
Ctrl-p-q
ps aux | grep 321
docker attach <ID>
Ctrl-c
touch hello.txt
Ctrl-p-q
sudo find /mnt -name "hello.txt"
sudo ls /mnt/..../diff/....
sudo ls /mnt/..../mnt/...
docker logs <ID>
docker diff <ID>
docker commit <ID> touched
docker stop <ID>
docker images
docker run -it --rm touched
ls

eval $(docker-machine env node-1)
export | grep DOCKER
docker images
docker pull websphere-liberty:webProfile7
docker images
docker history websphere-liberty:webProfile7
docker run -d -p 9080:9080 websphere-liberty:webProfile7
docker logs --tail=all -f <ID>
docker ps
docker-machine ip node-1
<BROWSE IP:PORT>
docker rm -f <ID>
docker run -d -P -v $(pwd)/ServletApp.war:/config/dropins/app.war websphere-liberty:webProfile7
docker logs --tail=all -f <ID>
docker port <ID>
curl <IP>:<PORT>/app
docker rm -f <ID>
cat Dockerfile
docker build -t app .
docker run -d -P --name hello app
docker logs --tail=all -f hello
docker port hello 9080
curl <IP>:<PORT>/app
docker rm -f hello

cd ../swarm
docker swarm init --advertise-addr <IP>
docker $(docker-machine config node-2) swarm join ....
docker $(docker-machine config node-3) swarm join ....
docker info
docker service create --name ferret -p 9080:9080 wasdev/ferret:1.1
docker service ps ferret
docker $(docker-machine config <node>) ps
docker-machine ip <node>
<BROWSE <IP>:9080/ferret>
<BROWSE <ANOTHER_IP>:9080/ferret>
docker service scale ferret=3
docker service ps ferret
curl <ip>:9080/ferret/ |& grep -A 1 localHost
curl <ip>:9080/ferret/ |& grep -A 1 localHost
curl <ip>:9080/ferret/ |& grep -A 1 localHost
docker service update --image wasdev/ferret:1.2 --update-delay 30s --update-parallelism 1 ferret
docker service ps ferret
curl <ip>:9080/ferret/ |& grep css
curl <ip>:9080/ferret/ |& grep css
docker stack deploy --compose-file compose.yml mongoapp
docker stack ps mongoapp
vim compose.yml
docker service inspect mongoapp_web
curl <IP>:<PORT>/mongoDBApp

cd ../kube
eval $(minikube docker-env)
docker ps
vim deployment.yml
kubectl create -f deployment.yml
minikube dashboard
kubectl expose deployment ferret --type=NodePort
minikube service ferret
vim deployment.yml - update image to wasdev/ferret:latest
kubectl apply -f deployment.yml
kubectl rollout status deployments ferret
<REFRESH BROWSER>
