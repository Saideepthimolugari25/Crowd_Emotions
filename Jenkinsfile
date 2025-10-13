pipeline {
    // Run this pipeline only on the Windows slave agent
    agent { label 'win' }

    environment {
        VENV = "${WORKSPACE}\\venv"
    }

    stages {

        stage('Checkout') {
            steps {
                echo "Cloning the repository..."
                git url: 'https://github.com/yourusername/crowd-emotion-detection.git', branch: 'main'
            }
        }

        stage('Setup Python Environment') {
            steps {
                echo "Setting up Python virtual environment on Windows..."
                bat """
                    python -m venv %VENV%
                    %VENV%\\Scripts\\pip install --upgrade pip
                    %VENV%\\Scripts\\pip install -r requirements.txt
                """
            }
        }

        stage('Run Tests') {
            steps {
                echo "Running tests..."
                bat """
                    %VENV%\\Scripts\\pytest.exe tests
                """
            }
        }

        stage('Run Emotion Detection') {
            steps {
                echo "Running Crowd Emotion Detection..."
                bat """
                    %VENV%\\Scripts\\python.exe main.py
                """
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully on Windows agent!"
        }
        failure {
            echo "Pipeline failed on Windows agent."
        }
    }
}
