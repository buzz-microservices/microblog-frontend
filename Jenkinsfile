pipeline {
  agent none
  options { 
    buildDiscarder(logRotator(numToKeepStr: '5'))
    skipDefaultCheckout true
  }
  stages
  {
    stage('Build image'){
      agent {
        kubernetes{
          label 'kaniko'
        }
      
      steps {
            checkout scm           
            container(name: 'kaniko-container', shell: '/busybox/sh') {
              sh '''
                 /kaniko/executor --context `pwd` --destination gcr.io/microblog-from-kaniko:latest
                 '''
            }
      } 
    }
    }
  }
}
