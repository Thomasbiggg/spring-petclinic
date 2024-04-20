pipeline {
    agent any

    stages {
        // Make sure each build starts with a clean state
        stage('Clean Workspace') {
            steps {
                cleanWs()
            }
        }

        // To check out the source code from a Git repository so that it can be used in the later stages of the pipeline
        stage('Git Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Thomasbiggg/spring-petclinic.git']])
                echo 'Git Checkout Completed'
            }
        }

        // // To perform static code analysis on the checked-out source code using SonarQube, which is a tool for continuously inspecting code quality and security vulnerabilities.
        // stage('SonarQube Analysis') {
        //     steps {
        //         withSonarQubeEnv('sonarqube') {
        //             sh 'mvn clean package sonar:sonar'
        //             echo 'SonarQube Analysis Completed'
        //         }
        //     }
        // }
        stage('Build Application') {
            steps {
                sh 'mvn clean package'
            }
        }

        // To build the project with Maven, run the resulting JAR file to start the application, wait for a certain period (1 min) for the application to run, and then shut it down.
        stage('Deploy Application') {
            steps {
                script {
                    ansiblePlaybook(
                        playbook: '/var/jenkins_home/ansible/playbook.yml',
                        inventory: '/var/jenkins_home/ansible/inventory.ini',
                        extraVars: [
                            "workspace": env.WORKSPACE
                        ]
                    )
                }
            }
        }
    }
}