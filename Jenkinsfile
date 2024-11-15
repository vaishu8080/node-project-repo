pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
        
        stage('Check npm Installation') {
            steps {
                script {
                    def npmInstalled = sh(script: 'command -v npm', returnStatus: true) == 0
                    if (!npmInstalled) {
                        echo 'npm is not installed. Installing npm...'
                        sh 'sudo apt update && sudo apt install -y npm'
                    } else {
                        echo 'npm is already installed.'
                    }
                }
            }
        }
        
        stage('Run npm Test') {
            steps {
                sh 'npm test'
            }
        }
        
        stage('Run npm Build') {
            steps {
                sh 'npm run build'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
