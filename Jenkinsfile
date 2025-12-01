pipeline {
    agent any
    
    environment {
        API_TOKEN = credentials('token') // ID you set in Jenkins
    }

    parameters {
        choice(
            name: 'SUITE',
            choices: ['uiErrorValidation', 'HybridE2ETest', 'API_ErrorValidation', 'Login', 'Registration'],
            description: 'Select which test suite to run'
        )
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Run Selected Test Suite') {
            steps {
                bat "mvn clean test -P%SUITE%"
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/test-output/**/*', allowEmptyArchive: true
        }
    }
}
