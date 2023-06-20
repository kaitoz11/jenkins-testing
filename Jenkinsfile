pipeline {
    agent any

    tools {

        nodejs 'node 18.16.0'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/kaitoz11/jenkins-testing.git'
            }
        }

        stage('Build') {
            steps {
                sh 'npm ci'
            }
        }

        stage('Test') {
            steps {
                sh 'npm run test'
            }
        }

        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'sonar scanner'
            }
            steps {
                withSonarQubeEnv(credentialsId: 'sonar_secret', installationName: 'sonar_server') {
                    sh "${scannerHome}/bin/sonar-scanner -D sonar.projectKey=swt_testing"
                }
            }
        }
    }
}
