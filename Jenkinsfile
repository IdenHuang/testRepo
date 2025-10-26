pipeline {
    agent any

    environment {
        PYTHON = 'python3'  // You can change this if your Python installation has a different name
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your Git repository
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                // Optional: Install dependencies from requirements.txt if needed
                sh "${env.PYTHON} -m pip install --upgrade pip"
                sh "${env.PYTHON} -m pip install -r requirements.txt || true"
            }
        }

        stage('Run Test Orchestrator') {
            steps {
                sh "${env.PYTHON} test_orchestrator.py --regression"
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