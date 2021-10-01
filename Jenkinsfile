pipeline {
    agent any
    tools
    {
	jdk 'java11'
       maven 'maven3.8.2'
       
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
    }
}
