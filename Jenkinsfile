pipeline {
    agent any
    environment {
       AWS_ACCOUNT_ID = '118716265887';
       AWS_REGION = 'ap-south-1';
       AWS_REPO_URI = '118716265887.dkr.ecr.ap-south-1.amazonaws.com/docker-deploy-1';
       AWS_REPO_NAME = 'docker-deploy-1';
       IMAGE_REPO_NAME = 'docker-image-aws';
       IMAGE_TAG = 'latest';
    }
    stages {
        stage('Git Checkout') {
            steps {
                checkout scm
            }
        }
        stage ('Docker Build') {
            steps {
               script{
                dockerImage = docker.build "${IMAGE_REPO_NAME}:${IMAGE_TAG}"
               }
            }
        }
        stage ('AWS Login') {
            steps {
               sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 118716265887.dkr.ecr.ap-south-1.amazonaws.com/docker-deploy-1'
            }
        }
        stage ('AWS Deploy') {
            steps {
                sh "docker tag ${IMAGE_REPO_NAME}:${IMAGE_TAG} ${AWS_REPO_URI}:${IMAGE_TAG}"
                sh "docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${AWS_REPO_NAME}:${IMAGE_TAG}"
            }
        }
        stage('Stage 4') {
            steps {
                echo 'Hello New Stage3!!!!'
            }
        }
    }
}
