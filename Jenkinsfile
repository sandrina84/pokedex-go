pipeline {
    // facultative
    environment {
        BUILD_SCRIPTS_GIT="http://10.100.100.10:7990/scm/~myname/mypipeline.git"
        BUILD_HOME='/var/lib/jenkins/workspace'
    }
    parameters {
        // Can be onelined, but displayed with space for readability
        string(
            name: "BUILD_SCRIPTS",
            defaultValue: "mypipeline",
            description: "Build script to use"
        )
    }
    agent any
    stages {
        stage('Checkout: Code') {
            steps {
                checkout scm
                sh """chmod -R +x ${params.BUILD_SCRIPTS}"""
            }
        }
        stage('Yum: Updates') {
            steps {
                sh "${params.BUILD_SCRIPTS}/scripts/update.sh"
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}