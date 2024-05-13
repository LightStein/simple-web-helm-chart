pipeline {
    agent any
    parameters {
        choice(name: 'ACTION', choices: ['deploy', 'default', 'destroy'], defaultValue: 'default', description: 'Select action or default for automatic deploy')
    }
    environment {
        KUBECONFIG = '/home/azureuser/.kube/config'
        IS_MANUAL = "${params.ACTION != 'default'}"  // Evaluates to true if action is explicitly chosen
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
                    if (env.IS_MANUAL == 'false' || params.ACTION == 'deploy') {
                        echo "Deploying..."
                        sh 'helm upgrade --install simple-web-release . --namespace thomas'
                    } else if (params.ACTION == 'destroy') {
                        echo "Destroying..."
                        sh 'helm delete simple-web-release -n thomas'
                    } else {
                        echo "Default action taken: Deploying..."
                        sh 'helm upgrade --install simple-web-release . --namespace thomas'
                    }
                }
            }
        }
    }
}
