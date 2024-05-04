pipeline {
  environment {
    dockerimagename = "prathaban1994/myreactapp:tagname"
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
          dockerImage = docker.build('dockerimagename', '-f Dockerfile .')
        }
      }
    }
    stage('Pushing Image') {
      environment {
          registryCredential = 'dockerhub'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }
    stage('Deploying React.js container to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", 
                                         "service.yaml")
        }
      }
    }
  }
}
