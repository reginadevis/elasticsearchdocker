Steps to run this application

1) Please install Docker desktop and WSL2 (in case the OS is Windows 10 Home version), else please enable Hyper V mode in Windows Features.
2) After packaging the application through maven, please open powershell and go the directory where 'Dockerfile' is present.
3) Please follow the below steps in powershell.

//docker run elasticsearch

docker container run --network sample -p 9200:9200 -p 9300:9300 --name trialsearch -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.12.1

//dockeer run sample elastic image

docker image build -t elastic .

docker container run --network sample --name accident-container -p 8080:8080 -d elastic

docker container logs -f accident-container

Note: If the system memory is exhausted due to docker desktop, the below steps can be performed to increase the processors and heap size for WSL.

1) In powershell, execute the below command.
      wsl --shutdown

2) Under C:/Users/<<myprofile>>, create the file '.wslconfig' and paste the below configurations.

[wsl2]
memory=4GB # Limits VM memory in WSL 2 to 4 GB
processors=2 # Makes the WSL 2 VM use two virtual processors

3) In powershell, execute the below command.
    wsl 

Note: Ensure docker is not running while performing these steps.

