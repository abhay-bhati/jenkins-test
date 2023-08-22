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
       CLUSTER_NAME = 'eks-2'
    }
    stages {
        stage('Git Checkout') {
            steps {
                checkout scm
            }
            // post {
            //     always {
            //         echo "AAlways: ${env.JOB_NAME}"
            //         echo "2: ${env.BUILD_NUMBER}"
            //         echo "3: ${env.status}"
            //         echo "4: ${env.details}"
            //         echo "5: ${env.DETAILS}"
            //     }
            //     failure {
            //         echo "FFajilure"
            //     }
            // }
        }
        // stage ('Docker Build') {
        //     steps {
        //        script{
        //         dockerImage = docker.build "${IMAGE_REPO_NAME}:${IMAGE_TAG}"
        //        }
        //     }
        // }
        // stage ('AWS Login') {
        //     steps {
        //        sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 862839345820.dkr.ecr.ap-south-1.amazonaws.com/docker-deploy-1:latest'
        //     }
        // }
        // stage ('AWS Deploy') {
        //     steps {
        //         sh "docker tag ${IMAGE_REPO_NAME}:${IMAGE_TAG} ${AWS_REPO_URI}:${IMAGE_TAG}"
        //         sh "docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/${AWS_REPO_NAME}:${IMAGE_TAG}"
        //     }
        // }
        // stage('Stage 4') {
        //     steps {
        //         sh "aws eks update-kubeconfig --region ${AWS_REGION} --name ${CLUSTER_NAME}"
        //         sh "kubectl apply -f deployment.yaml"
        //         sh "kubectl apply -f service.yml"
        //     }
        // }
         stage('Publish on Playstore'){
            steps{
                androidApkUpload googleCredentialsId: params.accountName, apkFilesPattern: "app.aab", trackName: 'production', rolloutPercentage:'100'
            }
            post {
                success {
                    echo "Scucess"
                }
                failure {
                    echo "Failure"
                    echo ${err}
                }
            }
         }
        // 
        // try {
        //                        androidApkUpload googleCredentialsId: params.accountName, apkFilesPattern: "app.aab", trackName: 'production', rolloutPercentage:'100'

        // }
        // catch(err) {
        //     echo "cauthg: ${err}"
        // }
        // stage('Slack Notifs') {
        //     steps {
        //         slackSend color: "#FFFF00", message: "Slack Notifs by Abhay"
        //     }
        // }
    }
        // post{
        //     always {
        //         echo "Always: ${env.BUILD_NUMBER}"
        //     }
        //     failure {
        //         echo "Failure"
        //     }
        // }
}
