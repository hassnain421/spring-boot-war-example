pipeline {
    agent any
    tools
    {
       maven 'maven3.8.2'
       jdk 'java8'
    }

    stages {
	    stage('checkout') {
	        steps {
            git branch: 'master', url: 'https://github.com/hassnain421/spring-boot-war-example.git'
         }
        }
     	stage('Execute Maven') {

            steps {
                sh 'mvn clean install'
                    
                }
             }
	
        stage('Docker Build and Tag') {
            steps {
              
                sh 'docker build -t samplewebapp:latest .' 
                sh 'docker tag samplewebapp hassnain421/samplewebapp:latest'
                  }
               }
     
        stage('Publish image to Docker Hub') {
          
            steps {
                withDockerRegistry([ credentialsId: "dockerHub", url: "" ]) {
                        sh  'docker push hassnain421/samplewebapp:latest'
                    }
                    
                 }
              }
     
        stage('Run Docker container on Jenkins Agent') {
             
            steps 
			  {
                sh "docker run -d -p 8003:8080 hassnain421/samplewebapp:latest"
 
            }
        }
        stage('Run Docker container on remote hosts') {
             
            steps {
                sh "docker -H ssh://root@167.71.110.22 run -d -p 8003:8080 hassnain421/samplewebapp:latest"
 
            }
        }
    }
}
