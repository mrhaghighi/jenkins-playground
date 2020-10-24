pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh 'echo "Hello World!"'
            }
        }

        stage('deploy') {
            steps {
                retry(3) {
                    echo "Trying..."
                }

                timeout(time: 2, unit: 'MINUTES') {
                    echo "Health check: OK"
                }
            }
        }
    }

    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}