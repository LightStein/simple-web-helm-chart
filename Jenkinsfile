pipeline {
    agent any

    parameters {
        choice(name: 'ACTION', choices: ['default (deploy)', 'deploy', 'destroy'], description: 'Select action or default for automatic deploy')
    }

    environment {
        KUBECONFIG = '/home/azureuser/.kube/config'
    }

    stages {
        stage('Checkout') {
            steps {
                git(url: 'https://github.com/LightStein/simple-web-helm-chart.git', branch: 'main')
            }
        }

        stage('Deploy or Destroy') {
            steps {
                script {
                    if (params.ACTION == 'default (deploy)' || params.ACTION == 'deploy') {
                        echo "Deploying..."
                        sh 'helm upgrade --install simple-web-release . --namespace thomas'
                    } else if (params.ACTION == 'destroy') {
                        echo "Destroying..."
                        sh 'helm delete simple-web-release -n thomas'
                    }
                }
            }
        }
