pipeline {
    agent any

    environment {
        KUBECONFIG = credentials('kubeconfig') // Your Jenkins credential ID
    }

    stages {

        stage('Checkout Code') {
            steps {
                // Replace this URL with your GitHub repo URL
                git branch: 'main', url: 'https://github.com/poorna484/three_cont_pod.git'
            }
        }

        stage('Deploy Pod') {
            steps {
                sh '''
                export KUBECONFIG=$KUBECONFIG
                kubectl apply -f pod.yaml
                '''
            }
        }

        stage('Verify Pod') {
            steps {
                sh '''
                export KUBECONFIG=$KUBECONFIG
                kubectl get pods
                kubectl describe pod simple-multi-container-pod
                '''
            }
        }

        stage('View Logs') {
            steps {
                sh '''
                export KUBECONFIG=$KUBECONFIG
                echo "Logs from quote-container:"
                kubectl logs simple-multi-container-pod -c quote-container --tail=5
                echo "Logs from fortune-container:"
                kubectl logs simple-multi-container-pod -c fortune-container --tail=5
                echo "Logs from cowsay-container:"
                kubectl logs simple-multi-container-pod -c cowsay-container --tail=5
                '''
            }
        }
    }
}

