pipeline {
    agent any

    environment {
        VENV_DIR = "venv"
        REPO_NAME = "JenkinsFile-Python"
    }

    stages {
        stage('updated_Cleanup') {
            steps {
                echo 'Cleaning up old files if any...'
                sh 'rm -rf $REPO_NAME $VENV_DIR'
            }
        }

        stage('Clone Repository') {
            steps {
                echo 'Cloning GitHub repo...'
                sh 'git clone https://github.com/okanshuman/JenkinsFile-Python.git'
            }
        }

        stage('Create Virtual Environment') {
            steps {
                echo 'Creating virtual environment...'
                sh 'python3 -m venv $VENV_DIR'
            }
        }

        stage('Activate and Install Dependencies') {
            steps {
                echo 'Activating virtualenv and installing dependencies...'
                sh '''
                source $VENV_DIR/bin/activate
                pip install --upgrade pip
                '''
            }
        }

        stage('Run Python App') {
            steps {
                echo 'Running app.py...'
                sh '''
                source $VENV_DIR/bin/activate
                cd $REPO_NAME
                python3 app.py
                '''
            }
        }
    }
    
    post {
        always {
            echo 'Cleaning up virtual environment...'
            sh 'rm -rf $VENV_DIR'
        }
    }
}
