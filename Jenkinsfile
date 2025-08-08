pipeline {
    agent any

    environment {
        VENV_DIR = "venv"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install Python & Create venv') {
            steps {
                sh '''
                    python3 -m venv $VENV_DIR
                    . $VENV_DIR/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                    . $VENV_DIR/bin/activate
                    pytest
                '''
            }
        }

        stage('Run App') {
            steps {
                sh '''
                    . $VENV_DIR/bin/activate
                    python app.py
                '''
            }
        }
    }

    post {
        always {
            echo "Cleaning up..."
            sh 'rm -rf $VENV_DIR'
        }
    }
}
