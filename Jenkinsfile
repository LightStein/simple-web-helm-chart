pipeline {
    agent any

    parameters {
        choice(name: 'ACTION', choices: ['default (deploy)', 'destroy'], description: 'Select action or default for automatic deploy')
        string(name: 'VERSION', defaultValue: '', description: 'Specify the version to roll back to (only required for rollback action)')
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
                    if (params.ACTION == 'default (deploy)') {
                        echo "Deploying..."
                        sh 'helm upgrade --install simple-web-release . --namespace thomas'
                    } else if (params.ACTION == 'destroy') {
                        echo "Destroying..."
                        sh 'helm delete simple-web-release -n thomas'
                        currentBuild.result = 'SUCCESS'
                        return // Exit the pipeline after destroy
                    }
                }
            }
        }

        stage('Manual Approval') {
            when {
                expression {
                    params.ACTION == 'default (deploy)'
                }
            }
            steps {
                script {
                    def userInput = input(
                        id: 'UserInput', message: 'Check the deployment. What would you like to do next?',
                        parameters: [
                            choice(name: 'NEXT_ACTION', choices: 'Proceed\nRollback', description: 'Choose an action')
                        ]
                    )
                    env.USER_ACTION = userInput
                }
            }
        }

        stage('Roll Back') {
            when {
                expression {
                    return env.USER_ACTION == 'Rollback'
                }
            }
            steps {
                script {
                    def rollbackVersion = input(message: 'Enter the version to roll back to:', parameters: [string(name: 'VERSION', defaultValue: '', description: 'Specify the version to roll back to')])
                    echo "Rolling back to version ${rollbackVersion}..."
                    sh "helm rollback simple-web-release ${rollbackVersion} -n thomas"
                }
            }
        }
    }
}
