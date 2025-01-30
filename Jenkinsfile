pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/dedenfarhanhub/sample-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t my-node-app .'
            }
        }

        stage('Test') {
            steps {
                sh 'docker run --rm my-node-app npm test'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker tag my-node-app your-dockerhub-username/my-node-app'
                    sh 'docker push your-dockerhub-username/my-node-app'
                }
            }
        }

        stage('Deploy to Minikube') {
            steps {
                sh 'kubectl apply -f k8s/deployment.yaml'
            }
        }
    }
}
