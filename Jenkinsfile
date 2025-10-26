pipeline {
    agent any

    environment {
        PYTHON = 'python3'  // You can change this if your Python installation has a different name
    }

    stages {
        stage('Run Test Orchestrator') {
            steps {
                sh "${env.PYTHON} test_orchestrator.py --regression"
            }
        }
        stage('Results') {
            steps {
                script {
                    def log = currentBuild.rawBuild.getLog()
                    def result = log.find { it.contains('FAILURE')}
                }
                if (result) {
                    error ()
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline finished"
        }
        success {
            echo "Tests ran successfully!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}