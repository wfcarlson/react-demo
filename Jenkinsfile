pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh 'docker build -t react .'
            } 
        }
        stage('test') {
            steps {
                sh 'docker run -d react'
            }  
        }

        stage('deploy') {
            steps {
                sh 'aws configure set region us-east-1'
                sh 'aws ecr get-login --no-include-email | source /dev/stdin'
                sh 'docker tag react 090999229429.dkr.ecr.us-east-1.amazonaws.com/jenkins-demo'
                sh 'docker push 090999229429.dkr.ecr.us-east-1.amazonaws.com/jenkins-demo'
                sh 'aws ecs register-task-definition --cli-input-json file://task_definition.json'
                sh 'aws ecs create-service --cluster jenkins-cluster --service react-demo --task-definition jenkins-demo --desired-count 1'
            }
        }
    }
}
