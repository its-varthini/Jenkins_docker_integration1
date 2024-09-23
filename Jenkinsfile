pipeline {
    agent any
    
    tools {
      maven 'M3'
    }

    stages {
        stage('checkout') {
            steps {
                echo 'checkout code from git'
                git 'https://github.com/its-varthini/maven-web-app-ashokit.git'
            }
        }
        
         stage('build') {
            steps {
                echo 'build code using maven'
                sh 'mvn clean package'
            }
        }
        
        stage('docker build') {
            steps {
                echo 'build docker image'
                sh 'docker build -t mavenwebimage .'
            }
        }
        
        stage('docker deploy') {
            steps {
                echo 'build docker image'
                sh 'docker stop mywebapp'
                sh 'docker rm mywebapp'
                sh 'docker run -d --name mywebapp -p 9090:8080 mavenwebimage'
            }
        }
    }
}
