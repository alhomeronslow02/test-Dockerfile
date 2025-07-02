pipeline{
  agent any
  environment{
    IMAGE_NAME = 'alhomeronslow02/test-Dockerfile'
  }
  stages{
    stage('Checkout'){
      steps{
        git branch: 'main',
          url: 'https://github.com/alhomeronslow02/test-Dockerfile'
      }
    }
     stage('Build Docker image'){
      steps{
        sh script: "docker build -t %IMAGE_NAME%:latest ."
      }
    }
     stage('Push to Dockerhub'){
      steps{
        withCredential([usernamePasword(credentialsId: 'docker', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]){
          sh script: """ 
          echo %DOCKER_PASS% |
          docker login -u DOCKER_USER --password-stdin
          docker push %IMAGE_NAME%:latest
          docker logout
          """
        }
      }
    }
  }
}
