pipeline {
    agent any
    // tools {
    //     maven 'Maven'
    // }

    stages {
        stage('Git Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Thomasbiggg/spring-petclinic.git']])
                echo 'Git Checkout Completed'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'sonarqube scanner'; // 'SonarQube Scanner' is the name you've given to your SonarQube Scanner installation in Jenkins configuration
                    withSonarQubeEnv('sonarqube') { // 'YourSonarQubeServer' is the name you've given to your SonarQube server configuration in Jenkins
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=test -Dsonar.projectName='test' -Dsonar.host.url=http://localhost:9000"
                    }
                }
            }
        }
    }
}