pipeline {
  environment {
    dockerimagename = "prathaban1994/myreactapp"
    dockerImage = ""
  }
  agent any
  stages {
    stage('Checkout Source') {
      steps {
         git branch: 'main',credentialsId: 'github_credentials', url: 'https://github.com/prathab222/jenkins-k8s_deployment.git'
      }
    }
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build(dockerimagename, '-f Dockerfile .')
        }
      }
    }
    stage('Pushing Image') {
      environment {
          registryCredential = 'dockerhub'
           }
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }
    stage('Deploying React.js container to Kubernetes') {
      steps {
        script {
          sh "kubectl --kubeconfig=$KUBE_CONFIG apply -f deployment.yaml"
          sh "kubectl --kubeconfig=$KUBE_CONFIG apply -f service.yaml"
        }
      }
    }
  }
}
