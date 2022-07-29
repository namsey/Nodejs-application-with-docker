pipeline{
agent any
environment{
DOCKERHUB_CREDENTIALS=credentials('dockerhub')
}
stages{
  stage('gitclone'){
    steps{
      git: ''
   }
 }
  
  stage('build'){
    steps{
      sh 'docker build -t naman11/nodejs_app:latest'  
     }
  }

  stage('login'){
    steps{
      sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
    }
  }

  stage('push'){
    steps{
      sh 'docker push naman11/nodejs_app:latest'
    }
  }

post{
   always{
     sh 'docker logout'
   }
  }
 }
}
