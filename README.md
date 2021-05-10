**Steps to run this application**

1) Please install Docker desktop and WSL2 (in case the OS is Windows 10 Home version), else please enable Hyper V mode in Windows Features.
2) After packaging the application through maven, please open powershell and go the directory where 'Dockerfile' is present.
3) Please follow the below steps in powershell.


_//create a docker network_
docker network create -d bridge sample

_//list the networks_
docker network ls

_//docker run elasticsearch_

docker container run --network sample -p 9200:9200 -p 9300:9300 --name trialsearch -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.12.1

_//create docker image for the application_

docker image build -t elastic .

_// run the image in the same network as elastic search so that they can communicate_
_// docker compose should be used in terms of production mode. This is done here as docker desktop in Home edition is not able to create the images under same network_
docker container run --network sample --name accident-container -p 8080:8080 -d elastic

_//view logs of the running app_
docker container logs -f accident-container


**Note:** If the system memory is exhausted due to docker desktop, the below steps can be performed to increase the processors and heap size for WSL.

1) In powershell, execute the below command.
      wsl --shutdown

2) Under C:/Users/<<myprofile>>, create the file '.wslconfig' and paste the below configurations.

[wsl2]
memory=4GB # Limits VM memory in WSL 2 to 4 GB
processors=2 # Makes the WSL 2 VM use two virtual processors

3) In powershell, execute the below command.
    wsl 

Note: Ensure docker is not running while performing these steps.

