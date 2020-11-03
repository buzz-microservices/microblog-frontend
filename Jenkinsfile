pipeline {
  agent none
  options { 
    buildDiscarder(logRotator(numToKeepStr: '5'))
    skipDefaultCheckout true
  }
  stages('Node Stages')
  {

    stage('Build image'){
      agent {
        kubernetes{
          label 'kaniko'
        }
      }
      steps {
            checkout scm           
            container(name: 'kaniko', shell: '/busybox/sh') {
              sh '''
                 /kaniko/executor --context `pwd` --destination gcr.io/microblog-from-kaniko:latest
                 '''
            }
      } 
    }
  }
}
