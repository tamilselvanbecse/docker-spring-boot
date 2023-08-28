pipeline {
    agent slave

    stages {
        stage('Code Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/tamilselvanbecse/docker-spring-boot']])
            }
        }
    }
}
