pipeline {
    // Force this pipeline to run on the Windows slave node
    agent { label 'win-slave' }

    environment {
        DEPLOY_DIR = "C:\\flask_deploy_slave"
        PYTHON = "C:\\Users\\manda\\AppData\\Local\\Programs\\Python\\Python312"  // or your Python path
        PATH = "${PYTHON};${PYTHON}\\Scripts;${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Checking out source code on slave node..."
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                bat """
                    echo Installing Python dependencies globally...
                    pip install --upgrade pip
                    pip install -r requirements.txt
                """
            }
        }

        stage('Basic Check (Compile)') {
            steps {
                bat """
                    echo Running a basic syntax check for app.py...
                    python -m py_compile app.py
                """
            }
        }
    }

    post {
        success {
            echo "Flask pipeline on Windows slave completed successfully!"
        }
        failure {
            echo "Pipeline failed. Check console output on the slave node."
        }
    }
}
