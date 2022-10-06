pipeline {
    agent any

    stages {
        stage('Docker Build') {
            steps {
                sh 'aws ecr get-login-password --region eu-west-2 | sudo docker login --username AWS --password-stdin 101275806917.dkr.ecr.eu-west-2.amazonaws.com'
                sh 'sudo docker build -t 101275806917.dkr.ecr.eu-west-2.amazonaws.com/ecr-docker:latest .'
                sh 'sudo docker push 101275806917.dkr.ecr.eu-west-2.amazonaws.com/ecr-docker:latest'
            }
        }
         stage('Eks deploy') {
            steps {
                sh 'kubectl apply -f deployment.yaml service.yaml'       
            }
        }
         stage('validation') {
            steps {
                sh 'kubectl get po'
            }
        }
    }
}
