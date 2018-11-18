# Reference app with

- IntelliJ
- Gradle (Wrapper)
- SpringBoot
- MySql
- Docker
- bash scripts

What I still miss:

**app**
- can't connect from Java file to the database 
- no Hibernate integration

The app **doesn't** make use of **Docker plugin** to build an image and run in a container
and **doesn't** use **docker-compose**.

### NOTES:
- when referring to other files/folders we have to write the full path even if it's in the same folder, eg
./scripts/config.sh  or  ./gradlew clean   (where ./ means the root folder, gradlew is in the root folder)

- docker run nie kompiluje zmienionych plików - konieczny jest gradle build
- docker exec -it distracted_murdock /bin/sh (for alpine - which doesnt have bash or curl)
- docker exec -it distracted_murdock bash  (openjdk has bash and curl)

####This app uses bash scripts to build Docker containers for 
- the app 
- the database.

Run them like this **./ xxx.sh**
----------------------------
It's necessary to FIRST spin up the database with **db-up** if you want to use it in a container.
**db-up** - spins up the database in a Docker container
**db-down** - stops and destroys the container 

**run-all.sh**  
- builds the project with Gradle Wrapper
- builds the image
- connect to the db (it must be previously span up with **db-up** )
- runs the image WITHOUT the database in a Docker container
- removes the image and container when the server is stopped

**run-no-db.sh**  
As above but also
- doens connect to the db 

**run-skip-tests-no-db.sh**  
As **run.sh** but 
- doens connect to the db 
- skips tests
------------------
**./gradlew bootRun** - can be used to start the app outside Docker containers
**/gradlew clean build --info** - just build the JAR
**/gradlew clean test --scan** - just run unit tests
