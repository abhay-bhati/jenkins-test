pipeline {
    agent any
    environment {
       DOCKERHUB_CREDENTIALS = credentials('dockerhub');
    }
    stages {
        stage('Stage 1') {
            steps {
                checkout scm
            }
        }

        stage ('Docker Login') {
            steps {
               script{
                dockerImage = docker.build "test"
               }
            }
        }
         stage('Stage 3') {
            steps {
                echo 'Hello New Stage3!!!!'
                sh 'docker build -t docker-test-image .' 
            }
        }
    }
}
