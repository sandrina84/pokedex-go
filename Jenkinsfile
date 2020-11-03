pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout(
                    [
                        $class: 'GitSCM', 
                        branches: [[name: '**']], 
                        doGenerateSubmoduleConfigurations: false, 
                        extensions: [], 
                        submoduleCfg: [], 
                        userRemoteConfigs: [
                            [
                                credentialsId: '58d76b86-958b-49af-828c-0b0630a3fb22', 
                                url: 'https://github.com/sandrina84/pokedex-go.git'
                            ]
                        ]
                    ]
                )
            }
        }
        stage('Build') {
            steps {
                sh """docker build -t pokedex-go ."""
            }
        }
        stage('Test') {
            step npm test
        }
        stage('Deploy') {
            steps {
                sh """docker run --rm -p 5555:5555 pokedex-go:latest"""
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