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
          // sh 'docker run -d -p 5000:5000 anjireddy3993/flaskpro'
          sh 'docker push  anjireddy3993/flaskpro:latest '
      }
   
    }
  }
  stage(" kubectl run commands   "){
    steps{
       withKubeConfig(caCertificate: '', clusterName: 'kubernetes', contextName: 'kubernetes-admin@kubernetes', credentialsId: 'k8file', namespace: '', restrictKubeConfigAccess: false, serverUrl: ' https://192.168.122.31:6443') {
          sh 'kubectl get nodes'
          sh ' kubectl get pods'
          // sh 'kubectl apply -f dp3.yaml'
          // sh 'kubectl apply -f pod.yaml '
          sh 'kubectl apply -f nginx1.yaml'
           sleep(time: 200, unit: "SECONDS")
          sh 'kubectl port-forward  nginx1  5001:5000 '
    }



    }
  }  


}    
}

