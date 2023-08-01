pipeline {
    agent any
    environment {
       AWS_ACCOUNT_ID = '862839345820';
       AWS_REGION = 'ap-south-1';
       AWS_REPO_URI = '862839345820.dkr.ecr.ap-south-1.amazonaws.com/docker-deploy-1';
       AWS_REPO_NAME = 'docker-deploy-1';
       IMAGE_REPO_NAME = 'docker-image-aws';
       IMAGE_TAG = 'latest';
       PROFILE = 'abhay121'
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
               sh 'aws ecr get-login-password --profile abhay121 --region ap-south-1 | docker login --username AWS --password-stdin 862839345820.dkr.ecr.ap-south-1.amazonaws.com/docker-deploy-1:latest'
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
