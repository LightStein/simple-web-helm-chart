pipeline {
  agent any
  parameters {
      choice(name: 'ACTION', choices: ['deploy', 'destroy'], description: 'Select whether to deploy or destroy the helm deployment')
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
              if (params.ACTION == 'deploy') {
                  sh 'helm upgrade --install simple-web-release ./simple-web-helm-chart --namespace thomas'
              } else if (params.ACTION == 'destroy') {
                  sh 'helm delete simple-web-release -n thomas'
              }
          }
      }
    }
  }
  environment {
    KUBECONFIG = '/home/azureuser/.kube/config'
  }
}