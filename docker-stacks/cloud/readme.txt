I have created 4 docker compose files for cloud stack as mentioned below:

a) docker-compose.yml
b) docker-compose.override.yml       
c) docker-compose.test.yml
d) docker-compose.prod.yml

docker-compose.yml and docker-compose.override.yml files will be used for local development 

Command to run:    docker-compose up -d    (this command will use docker-compose.yml and docker-compose.override.yml files)

docker-compose.test.yml will be used in future when we will have our CI (for testing)

Command to run:  docker-compose -f docker-compose.yml -f docker-compose.test.yml up -d

Now for production, instead of docker-compose we will use docker stack deploy as docker-compose is not made for production.

So for production in order to generate the yml file, we have to use below command:

docker-compose -f docker-compose.yml -f docker-compose.prod.yml config > prodoutput.yml

Before running prodoutput.yml, we need to add labels which are being used in docker-compose.prod.yml file which restricts services to run on specific nodes.


Command to addd labels (run on docker swarm manager) : docker node update --label-add nginx=true node1

And prodoutput.yml will be the final yml file for production deployment, which can be deployed using below command:

docker stack deploy -c prodoutput.yml snw-cloud-app


Note: snw-cloud-app is the application name which can be any name
