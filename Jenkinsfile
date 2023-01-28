pipeline {
agent any 
stages {
   stage("checkout github"){
     steps{
       checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/rritsoft/cicd-docker-kubernetes-project.git']])

     }
   }
  stage(" docker build and push image") {
    steps{

      withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerhubPassword', usernameVariable: 'dockerhubUser')]) {
          sh 'docker build -t  anjireddy3993/flaskpro:latest   .'
          sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPassword}"
          sh 'docker push  anjireddy3993/flaskpro:latest '

       

      }

    
    }
  }



}    
}
