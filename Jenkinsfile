pipeline {
    agent any

    environment {
        FIREBASE_TOKEN = credentials('FIREBASE_TOKEN')
        PATH = "/usr/local/bin:/usr/bin:/bin"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/sureeporn-sudo/devopsSQA113-G1.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo $PATH'
                sh 'which node'
                sh 'which npm'
                sh 'which firebase'
                sh 'node -v'
                sh 'npm -v'
                sh 'npm install -g firebase-tools'
                sh 'firebase --version'
            }
        }

        stage('Testing') {
            steps {
                sh 'firebase use testing'
                sh 'firebase deploy --token "$FIREBASE_TOKEN"'
            }
        }

        stage('Staging') {
            steps {
                sh 'firebase use staging'
                sh 'firebase deploy --token "$FIREBASE_TOKEN"'
            }
        }

        stage('Production') {
            steps {
                sh 'firebase use production'
                sh 'firebase deploy --token "$FIREBASE_TOKEN"'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check logs.'
        }
    }
}