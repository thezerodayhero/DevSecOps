pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/thezerodayhero/DevSecOps.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    docker.build('DevSecOps')
                }
            }
        }
        stage('Test') {
            steps {
                sh 'docker run DevSecOps test-command'
            }
        }
        stage('Security Scan') {
            steps {
                sh 'snyk test --all-projects'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d DevSecOps'
            }
        }
    }
    post {
        always {
            sh 'docker rmi DevSecOps'
        }
    }
}
