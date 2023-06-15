####
            
![preview](./12.png)

        curl -fsSL https://test.docker.com -o test-docker.sh
        sh test-docker.sh
		
        sudo chmod 777 /var/run/docker.sock
        sudo usermod -aG docker ubuntu
		
		Exit the instance ...and relogin

        Multi Stage Docker build
        Multi staged build is used to build the code and copy necessary files into the final stage which will be your image.
![priview](./13.png)

        Multi-stage builds link https://docs.docker.com/build/building/multi-stage/

        Scenario – 1: Java Spring petclinic

        To build this application we need
        jdk17
        maven
        git

        Manual steps:
    
         ` git clone https://github.com/spring-projects/spring-petclinic.git `
         ` cd spring-petclinic `
        mvn package ----once you dothis creating jar file...
        # a file gets created in target/spring-petclinic-*.jar

        
         Dockerfile....
          
          ` mkdir spc `
          ` cd spc `
          ` vi Dockerfile `
           
        ###
           FROM maven:3-amazoncorretto-17 AS builder
           RUN git clone https://github.com/spring-projects/spring-petclinic.git
           RUN cd spring-petclinic && mvn pacage
    
           FROM amazoncorretto-17-alpine-jdk
           LABEL author="raju"
           EXPOSE 8080
           ARG HOME_DIR=/spc
           WORKDIR ${HOME_DIR}
           COPY --from=builder /spring-petclinic/target/spring-*.jar ${HOME_DIR}/spring-petclinic.jar
           EXPOSE 8080
           CMD ["java',"jar","spring-petclinic-jar"]

           ###

         ` docker image build -t spc:3.0.0 . `
![preview](18.png)

         ` docker container run -it maven:3-amazoncorretto-17 /bin/bash `
![preview](19.png)

         ` docker container rm -f $(docker container ls -a -q) `
         ` docker image rm -f $(docker image ls -a -q)
![priview](20.png)
         
         

        To run this application we need jdk 17
      
        https://github.com/asquarezone/DockerZone/commit/968357bc0da234840996e75b3394811715bc35a9
              for the changes done to create spring petclinic as multistage build.

          Dockerfile....

         ### 
             FROM ubuntu AS generator
             RUN mkdir /test && touch test/{1..10}.text

             FROM alpine
             COPY --from=generator /test /test
             CMD ["sleep","1d"] 
         ###

        ` docker image build -t exp .  `
![privew](14.png)
         

         ` docker container run -it ubuntu:20.04 /bin/bash `
![privew](15.png) 

         ` apt update `
         ` apt install unzip `
         ` apt install wget `
         ` wget https://github.com/nopSolutions/nopCommerce/releases/download/release-4.60.3/nopCommerce_4.60.3_NoSource_linux_x64.zip

         ` apt install wget `

         ` ls `
         ` unzip nopCommerce_4.60.3_NoSource_linux_x64.zip `
![preview](16.png)
![preview](17.png)
          ` ls ` ----first
         `  rm nopCommerce_4.60.3_NoSource_linux_x64.zip `
         ` ls ` -----second
               
                  1 & 2 showing same result so we instaling unnessasary files
          





