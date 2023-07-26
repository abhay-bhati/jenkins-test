pipeline {
    agent any 
    environment {
       DOCKERHUB_CREDENTIALS = credentials('dockerhub');
    }
    stages {
        stage('Stage 1') {
            steps {
                echo 'Hello New Stage 1!!!'
                echo 'clone the repo'
                sh 'rm -fr cd ~/Desktop/jenkins-test'
                sh 'cd ~/Desktop && git clone git@github.com:abhay-bhati/jenkins-test.git'
            }
        }
        stage('Stage 2') {
            steps {
                echo 'Hello New Stage 2!!!'
                sh 'cd ~/Desktop/jenkins-test && git pull origin main'
            }
        }
        stage ('Docker Login') {
            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
        }
         stage('Stage 3') {
            steps {
                echo 'Hello New Stage3!!!!'
                sh 'docker build -t docker-test-image .' 
            }
        }
    }
}
