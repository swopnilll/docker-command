docker run hello-world

docker run busybox echo hi there
docker run busybox echo bye there
docker run busybox echo hello world
docker run busybox ls

docker ps // list all the running container
docker ps --all // list all the containers

docker run busybox ping google.com // this container continues running 

docker create hello-world
docker start -a <container-id> 

docker start <container-id> 
docker start -a <container-id>

docker logs <container-id> 

docker system prune 

docker create busybox echo hi there
// 370d965f51f6112a179e00348984eb934409e527ea78108953f15e37c1819170

docker start 370d965f51f6112a179e00348984eb934409e527ea78108953f15e37c1819170
// 370d965f51f6112a179e00348984eb934409e527ea78108953f15e37c1819170

docker logs 370d965f51f6112a179e00348984eb934409e527ea78108953f15e37c1819170
// hi there

docker create busybox ping google.com
docker start <container-id>
docker logs <container-id>

docker stop <container-id>
docker kill <container-id>

docker run redis
// ready to accept connections tcp

redis-cli
// command not found

docker exec -it <container-id> <command>

docker exec -it <container-id> redis-cli
// second command is run on the same container

docker exec -it <container-id> sh

docker run -it <image-name> sh






