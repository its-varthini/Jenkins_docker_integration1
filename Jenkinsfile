pipeline {
    agent any
    
    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"
        DOCKERHUB_CREDENTIALS= credentials('docker_cred')
    }
    
    tools {
      maven 'M3'
    }

    stages {
        stage('checkout') {
            steps {
                echo 'checkout code from git'
                //git 'https://github.com/its-varthini/Jenkins_docker_integration1.git'
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/its-varthini/Jenkins_docker_integration1.git']]])
               
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
               // sh 'docker build -t mavenwebimage .'
                sh 'docker build -t varthinidochub/cicd-e2e:${BUILD_NUMBER} .'
            }
        }
        
        stage('Login to Docker Hub') {      	
            steps{                       	
            	sh '''
            	docker login --username=$DOCKERHUB_CREDENTIALS_USR --password=$DOCKERHUB_CREDENTIALS_PSW              		
            	echo 'Login Completed' 
            	'''
            }           
        }
        
        stage('Push the artifacts'){
           steps{
                script{
                    sh '''
                    echo 'Push to Repo1'
                    docker push varthinidochub/cicd-e2e:${BUILD_NUMBER}
                    
                    '''
                }
            }
        }
        
       
        
    }
}
