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
                sh '/usr/local/bin/node -v'
                sh '/usr/local/bin/npm -v'
                sh '/usr/local/bin/npm install -g firebase-tools'
                sh '/usr/local/bin/firebase --version'
            }
        }

        stage('Testing') {
            steps {
                sh '/usr/local/bin/firebase use testing'
                sh '/usr/local/bin/firebase deploy --token "$FIREBASE_TOKEN"'
            }
        }

        stage('Staging') {
            steps {
                sh '/usr/local/bin/firebase use staging'
                sh '/usr/local/bin/firebase deploy --token "$FIREBASE_TOKEN"'
            }
        }

        stage('Production') {
            steps {
                sh '/usr/local/bin/firebase use production'
                sh '/usr/local/bin/firebase deploy --token "$FIREBASE_TOKEN"'
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