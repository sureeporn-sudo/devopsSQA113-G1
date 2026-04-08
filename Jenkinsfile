pipeline {
    agent any

    environment {
        FIREBASE_TOKEN = credentials('FIREBASE_TOKEN')
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
                sh 'npm install -g firebase-tools'
                sh 'firebase --version'
            }
        }

        stage('Testing') {
            steps {
                sh 'firebase use testing && firebase deploy --token "$FIREBASE_TOKEN"'
            }
        }

        stage('Staging') {
            steps {
                sh 'firebase use staging && firebase deploy --token "$FIREBASE_TOKEN"'
            }
        }

        stage('Production') {
            steps {
                sh 'firebase use production && firebase deploy --token "$FIREBASE_TOKEN"'
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