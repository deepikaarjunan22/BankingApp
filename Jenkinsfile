pipeline {
    agent { label 'master' }
    
    environment {
        DOCKERHUB_CREDENTIALS= credentials ('dockerhub')
    }

    stages {
        stage('SCM_Checkout') {
            steps {
                echo 'Clone the github repo'
                git 'https://github.com/deepikaarjunan22/BankingApp.git'
            }
        }
        stage ('Build using maven') {
            steps {
                echo 'build using maven'
                sh 'mvn clean package'
            }
        }
        stage ('docker build') {
            steps {
                echo 'build docker image'
                sh 'docker build -t deepikaarjunan/hello-world:v1 . '
                sh 'docker image list'
            }
        }
        stage ('docker login') {
            steps {
                echo 'docker login'
                sh ' echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage ('push the docker image') {
            steps {
                echo 'docker push'
                sh 'docker push deepikaarjunan/hello-world:v1'
            }
        }
    }
}
