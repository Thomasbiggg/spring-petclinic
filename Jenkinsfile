pipeline {
    agent any

    tools {
        maven 'Maven-Tool'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Thomasbiggg/spring-petclinic.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar-jenkins') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }

    post {
        always {
            deleteDir()
        }
    }
}