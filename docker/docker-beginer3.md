# Docker Compose


Docker Compose is a tool that allow you to describe (in a YAML file) and manage (with command lines) multiple containers as a set of inter-connected services.





## Démo


https://github.com/jirkapinkas/spring-boot-postgresql-docker-compose

docker run -it --rm --name my-maven-project -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven -v /var/run/:/var/run/ maven mvn clean install​

cd src/main/docker​

docker-compose up​

docker-compose down​

« depends_on »​

« restart: always » pour image app ​

docker-compose up -d​

docker ps​

Restart Docker​

docker ps​
