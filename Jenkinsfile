pipeline {
    agent any
    stages {
        stage('Pull Code From GitHub') {
            steps {
                git 'https://github.com/Libin05/K8s-testproject.git'
            }
        }
        stage('Build the Docker image') {
            steps {
                sh 'sudo docker build -t k8simage /var/lib/jenkins/workspace/K8s-project'
                sh 'sudo docker tag k8simage libin05/k8simage:latest'
                sh 'sudo docker tag k8simage libin05/k8simage:${BUILD_NUMBER}'
            }
        }
        stage('Push the Docker image') {
            steps {
                sh 'sudo docker image push libin05/k8simage:latest'
                sh 'sudo docker image push libin05/k8simage:${BUILD_NUMBER}'
            }
        }
        stage('Deploy on Kubernetes') {
            steps {
                sh 'kubectl apply -f /var/lib/jenkins/workspace/K8s-project/pod.yaml'
                sh 'kubectl rollout restart deployment loadbalancer-pod'
            }
        }
    }
}
