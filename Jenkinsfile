pipeline {
    agent {
        label "slave"
    }
    environment {
        registry = "669530358419.dkr.ecr.ap-south-1.amazonaws.com/my-docker-repo"
    }
    tools {
        maven "maven3"
    }

    stages {
        stage('Code Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/tamilselvanbecse/docker-spring-boot']])
            }
        }
        stage ("Build JAR") {
            steps {
                sh "mvn clean install"
            }
        }
        stage ("Build Image") {
            steps {
                script {
                    docker.build registry
                }
            }
       }
        stage ("Push to ECR") {
            steps {
                script {
                    sh "aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 669530358419.dkr.ecr.ap-south-1.amazonaws.com"
                    sh "docker push 669530358419.dkr.ecr.ap-south-1.amazonaws.com/my-docker-repo"
                    
                }
            }
        }
         stage ('Helm Deploy') {
          steps {
            script {
                sh "helm upgrade first --install mychart --namespace helm-deployment --set image.tag=latest"
                }
            }
        }
    }
}
