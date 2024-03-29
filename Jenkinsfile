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
            // steps {
            //     // Runs Maven build
            //     sh './mvnw package'
            // }
        

            steps {
                withSonarQubeEnv('sonarqube') {
                    sh 'mvn clean verify sonar:sonar' //port 9000 is default for sonar
                    echo 'SonarQube Analysis Completed'
                }
            }
        }
    }
}