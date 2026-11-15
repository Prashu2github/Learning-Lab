
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
                sh 'python3 -m pytest tests/ -v --junitxml=reports/test-results.xml'
            }
        }

        stage('Package Application') {
            steps {
                sh '''
                    mkdir -p dist
                    tar -czf dist/calculator-app.tar.gz app/calculator.py
                    echo "Application package created"
                    ls -lh dist/
                '''
            }
        }
    }

    post {
        always {
            echo 'Publishing test results...'
            junit allowEmptyResults: true,
                  testResults: 'reports/test-results.xml'

            echo 'Archiving build artifacts...'
            archiveArtifacts artifacts: 'dist/calculator-app.tar.gz,reports/test-results.xml',
                             allowEmptyArchive: true,
                             fingerprint: true
        }

        success {
            echo 'CI PIPELINE COMPLETED SUCCESSFULLY!'
        }

        failure {
            echo 'CI PIPELINE FAILED. Check the logs.'
        }
    }
}
