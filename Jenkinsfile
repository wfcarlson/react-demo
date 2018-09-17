pipeline {
    agent { docker { image 'node:6.3' } }
    stages {
        stage('test') {
            steps {
                sh 'npm run test'
            }
        }
        stage('build') {
            steps {
                sh 'npm --version'
            }
        }
    }
}
