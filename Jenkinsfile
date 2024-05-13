pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        git(url: 'https://github.com/LightStein/simple-web-helm-chart.git', branch: 'main')
      }
    }

  }
  environment {
    KUBECONFIG = '/home/azureuser/.kube/config'
  }
}