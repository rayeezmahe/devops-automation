pipeline{
    agent any
    tools{
        maven 'jenkins-maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/rayeezmahe/devops-automation']]])
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image'){
            steps{
                script{
                    sh 'docker build -t rayeezmahe/devops-automation .'
                }
            }
        }
        stage('Push Image to Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u rayeezmahe -p ${dockerhubpwd}'
                    }
                    sh 'docker push rayeezmahe/devops-automation'
                }
            }
        }
    }
}