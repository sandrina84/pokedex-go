pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh docker build -t pokedex-go .
            }
        }
        stage('Test') {
            step npm test
        }
        stage('Deploy') {
            steps {
                sh docker run --rm -it -p 5555:5555 pokedex-go:latest
                npm start
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}