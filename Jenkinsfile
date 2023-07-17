pipeline {
  agent any
  environment {
       DOCKERHUB_CREDENTIALS = credentials('docker-hub-sankar')
       PATH =  "/opt/apache-maven-3.9.2/bin:$PATH"
  }
  stages {
    stage('compile image'){
      steps{
        sh "mvn package"
      }
    }
    stage('Building image') {
      steps{
          sh "docker build -t sankar0812/cicd-demo:$BUILD_NUMBER ."
      }
    }
    stage('login to dockerhub'){
      steps{
          sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --pasword-stdin"
      }
    }
    stage('push images'){
      steps{
        sh "docker push sankar0812/cicd-demo:$BUILD_NUMBER"
      }
    }
}
post{
       always{
         sh "docker logout"
       }
    }
}

  
