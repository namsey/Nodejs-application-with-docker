pipeline {
  agent any
    environment {
      DOCKERHUB_CREDENTIALS=credentials('dockerhub')
    }
  stages {
    
    stage('Code Checkout') {
      steps{
        git 'https://github.com/namsey/Nodejs-application-with-docker.git'
    }
  }
  
  stage('Building Image') {
    steps{
      sh 'docker build -t naman11/nodejs_app:latest .'  
     }
  }

  stage('DockerHub Login') {
    steps{
      sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
    }
  }

  stage('Upload Image to DockerHub') {
    steps {
      sh 'docker push naman11/nodejs_app:latest'
    }
  }
  
  stage('Remove Image from Local Machine') {
    steps {
      sh 'docker rmi -f naman11/nodejs_app:latest'
    }
  }

  stage('Run Docker Container') {
    steps {
      sh 'docker run -it -d -p 8008:9005 naman11/nodejs_app:latest'
    }
  }

  stage('Verify Running Container') {
    steps {
      sh 'curl -X HEAD -I http://localhost:8008'
    }
  }

  stage('DockerHub Logout'){
    steps{
     sh 'docker logout'
   }
  }
 }
}
