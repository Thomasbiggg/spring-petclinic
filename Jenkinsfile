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

        // stage('SonarQube Analysis') {
        //     steps {
        //         withSonarQubeEnv('sonarqube') {
        //             sh 'mvn clean package sonar:sonar' //port 9000 is default for sonar
        //             echo 'SonarQube Analysis Completed'
        //         }
        //     }
        // }

        stage('Run') {
            steps {
                sh './mvnw package'
                sh 'nohup java -jar target/*.jar'
            }
        }
    }
}