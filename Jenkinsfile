pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Secret Scan') {
            steps {
                sh 'GITLEAKS_CONFIG=.gitleaks.toml gitleaks dir .'
            }
        }

        stage('Build') {
            steps {
                sh 'python3 --version'
                sh 'python3 -m py_compile app/app.py'
            }
        }
    }
}