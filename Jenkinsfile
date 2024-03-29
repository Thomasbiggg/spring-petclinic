pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Thomasbiggg/spring-petclinic.git']])
                echo 'Git Checkout Completed'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh 'mvn clean package sonar:sonar'
                    echo 'SonarQube Analysis Completed'
                }
            }
        }

        stage('Run') {
            steps {
                sh './mvnw package'
                sh '''
                    java -jar target/*.jar &
                    PID=$!
                    sleep 60 # wait for 1 minutes
                    kill $PID
                    '''
                echo 'Run and Exit Completed'
            }
        }
    }
}