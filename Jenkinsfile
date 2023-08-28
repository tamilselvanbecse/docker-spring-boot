pipeline {
    agent {
        label "slave"
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
    }
}
