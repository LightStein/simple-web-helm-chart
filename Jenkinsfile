pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/LightStein/simple-web-helm-chart.git', branch: 'main')
      }
    }

    stage('Deploy') {
      steps {
        sh 'helm upgrade --install simple-web-release ./simple-web-helm-chart --namespace thomas'
      }
    }

    stage('Destroy') {
      steps {
        sh 'helm delete simple-web-release -n thomas'
      }
    }

  }
  environment {
    KUBECONFIG = '/home/azureuser/.kube/config'
  }
}