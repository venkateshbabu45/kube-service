pipeline {
  agent any
  tools { 
        maven 'Maven'
        jdk 'Java'
  }
  stages {
    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace... */
      steps {
        checkout scm
      }
    }
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean package'
        sh 'echo $USER'
        sh 'echo whoami'
      }
    }
    
  stage('deploy to ECR') {
      steps {
        node('eks-master-node'){
          checkout scm
         sh 'kubectl apply -f deployment.yaml' 
         sh 'kubectl apply -f service.yaml' 
        }
      }
    } 
  }
}
