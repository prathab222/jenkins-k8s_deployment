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
        kubeconfig(caCertificate: 'LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSURCakNDQWU2Z0F3SUJBZ0lCQVRBTkJna3Foa2lHOXcwQkFRc0ZBREFWTVJNd0VRWURWUVFERXdwdGFXNXAKYTNWaVpVTkJNQjRYRFRJME1EVXdNakUyTkRjMU1Wb1hEVE0wTURVd01URTJORGMxTVZvd0ZURVRNQkVHQTFVRQpBeE1LYldsdWFXdDFZbVZEUVRDQ0FTSXdEUVlKS29aSWh2Y05BUUVCQlFBRGdnRVBBRENDQVFvQ2dnRUJBTU9JCjRYZmFvV1BGanJCeG43a3NacVROU3pXK3pOQmIvdG1zZk52OG9OaWhPRXNwamxWZDhEb1dReEZGUWJwY2dOUUUKZWRVR0wxMUZma1JLMm93by80UXgxTGJDWUYzSmwxV1AwQmU0Q00xNmJERnYyblM3aE5UMmdWa0VqVGJlL3IvVQpuMC8xUTFpcjFyZTlzTXN0NEtDQ1I5WmFOeFFWQTdiYVgrblBFemJ2WkVPMUtndFh4QUJvZGZ0UElCMU1MakFVCkMxbEFOaVdmU3d0emZkZmpaaTZHRk9zZ0gwbThmVCtqNVh2eXJ1UUIxQ1EwQlZVVnR0Tlpla3U3aE9WYy8xYysKbjdKNkU2WlBhTkhwVnVzZ0dUS2s4alliWERxeFdzam9RSG16enVRRitXanJFQW9zZC9oVy9CMkFOQVlNbG5sRwp4dDlJc0lyeWgyeFpGc085Z3lVQ0F3RUFBYU5oTUY4d0RnWURWUjBQQVFIL0JBUURBZ0trTUIwR0ExVWRKUVFXCk1CUUdDQ3NHQVFVRkJ3TUNCZ2dyQmdFRkJRY0RBVEFQQmdOVkhSTUJBZjhFQlRBREFRSC9NQjBHQTFVZERnUVcKQkJUQlBxWTEwYkE0dUlaM0Y5Nm9ENUxYU3BoUHpqQU5CZ2txaGtpRzl3MEJBUXNGQUFPQ0FRRUFlamJSSS9jUApRd2NUUThKaXB4ZVhoWmdVZUFhUzBVVmhCRWN1bW5jSXFzcVdnRmFqM0ZiQzVPbUs2cG5lV0pBWjZSaG1Wc2o1CjJvK01PRnJ3bHhMNmxUZ3BWckVSLzFhNXdsR0NScmJuSXV2RDcrM1IxdytCOWFOY2NramRiYmZydHhsbUFxZFYKOGdTTTM3Z09ud0VKZWpkQkNjQXlxR1FMTm13NkdML0c4ZnB1a0hvSlp3UTVOd204MHRDaUtBTG54MURpWFF3Zgo4c1MrdnVjNGVOSm5pY0JUVjY5dWJQOHA5N0hiUG1NcGJjVVRmcG5La2lRN3g4Wm1BRFJYS3lCVllCdmZFMVQ5CnJaR3NENEZieWpCMDFseW9KalJacko5M1I0UmVDSjh3NjA2YllsNnBaend0TXM0djZpOG5Mc3hhZ0pnU1Y2SDUKblp6N1lzQ0tvOHc4TlE9PQotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==', credentialsId: 'mykubeconfig', serverUrl: 'https://192.168.58.2:8443') {
          sh "kubectl apply -f deployment.yaml"
          sh "kubectl apply -f service.yaml"
        }
      }
    }
  }
}
