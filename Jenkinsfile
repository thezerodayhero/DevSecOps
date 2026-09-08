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
        
        stage('SAST') {
        steps {
            sh '/opt/semgrep-venv/bin/semgrep scan --config auto --error .'
        }
    }
        
        stage('SCA') {
            steps {
                sh '''
                    /opt/sca-venv/bin/pip-audit \
                    -r requirements.txt
                '''
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