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
    }
    
}