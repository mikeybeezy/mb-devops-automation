pipeline {
    agent any
    tools{
        maven 'Maven 3.8.6'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'MIK GITHUB SSH', url: 'https://github.com/mikeybeezy/mb-devops-automation']]])
                sh 'mvn clean install'
            }

        }
        stage('Buil Docker Image'){
            steps{
                script{
                    sh 'docker build -t mikeybabs/devops-integration .'
                   
                }
            }
        }
        stage('Push to Docker Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'Docker-Hub-Credentials', variable: 'DOCKER_HUB_PWD'), string(credentialsId: 'dockerhub username', variable: 'DOCKER_HUB_USERNAME')]) {
                    sh 'docker login -u "mikeybabs"  -p ${DOCKER_HUB_PWD}'
                    

                    sh 'docker push mikeybabs/devops-integration'

                    }
                }
            }
        }
        stage('Deploy to kubernetes'){
            steps{
                script{
                    sh 'kubectl apply -f deploymentservice.yaml'


                }
            }
        }
    }
    
}