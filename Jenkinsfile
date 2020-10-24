pipeline {
    agent { docker { image 'node:15.0.1' } }
    stages {
        stage('build') {
            steps {
                sh 'npm --version'
            }
        }
    }
}