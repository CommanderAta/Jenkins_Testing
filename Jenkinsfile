pipeline {
    agent any

    environment {
        // Replace with your Docker image name, e.g., "myapp:latest"
        DOCKER_IMAGE = 'myapp:latest' 
        // Adjust if your kubeconfig is located elsewhere
        KUBECONFIG = '/home/jenkins/.kube/config'
    }

    stages {
        // stage('Clone Repository') {
        //     steps {
        //         // Replace with your repository URL
        //         git url: 'https://your-git-repository-url.git', branch: 'master'
        //     }
        // }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        // stage('Push Docker Image') {
        //     steps {
        //         script {
        //             // Assuming Docker Hub, adjust for your container registry.
        //             // Replace 'docker-credentials-id' with your Jenkins credentials ID for Docker Hub.
        //             docker.withRegistry('https://index.docker.io/v1/', 'docker-credentials-id') {
        //                 docker.image("${DOCKER_IMAGE}").push()
        //             }
        //         }
        //     }
        // }

        stage('Deploy to Minikube') {
            steps {
                script {
                    // Assumes kubectl is configured to use Minikube context.
                    sh 'kubectl config use-context minikube'
                    // Replace 'deployment.yaml' with the path to your Kubernetes deployment file if different.
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }

    
}
