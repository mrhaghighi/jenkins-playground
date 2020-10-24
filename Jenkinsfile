pipeline {
    agent {
        docker {
            image 'node:15-alpine'
        }
    }

    environment {
        USERNAME = 'mrh_haghighi'
        PASSWORD = 'secret:)'
        COMMIT_ID = ''
    }

    stages {
        stage('preparation') {
            steps {
                script {
                    checkout scm
                    sh "git rev-parse --short HEAD > ./git/commit_id"
                    COMMIT_ID = readFile('./git/commit_id').trim()
                }
            }
        }

        stage('build') {
            steps {
                sh 'echo "Hello World!"'
            }
        }

        stage('test') {
            nodejs(nodeJSInstallationName: 'nodejs') {
                sh 'npm install --only=dev'
                sh 'npm test'
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

                echo "Your username is `${USERNAME}`"
                echo "Your password is `${PASSWORD}`"
                sh 'printenv'
            }
        }
    }

    post {
        always {
            script {
                echo 'This will always run'

                try {
                    junit 'build/reports/**/*.xml'
                } catch (error) {
                    echo "JUnit failed!"
                    echo "Catch error: ${error}"
                }
            }
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