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
        mvn package
        # a file gets created in target/spring-petclinic-*.jar


        To run this application we need jdk 17
      
        https://github.com/asquarezone/DockerZone/commit/968357bc0da234840996e75b3394811715bc35a9
              for the changes done to create spring petclinic as multistage build.

        