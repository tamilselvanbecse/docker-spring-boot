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
    }
}
