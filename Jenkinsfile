pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code checked out from GitHub'
            }
        }

        stage('Run Application') {
            steps {
                sh 'python3 app/calculator.py'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'python3 -m unittest discover -s tests -v'
            }
        }

        stage('Build Complete') {
            steps {
                echo 'Python Calculator CI Pipeline completed successfully!'
            }
        }
    }
}