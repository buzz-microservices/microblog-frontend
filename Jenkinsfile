pipeline {
  agent none
  options { 
    buildDiscarder(logRotator(numToKeepStr: '5'))
    skipDefaultCheckout true
  }
  stages('Node Stages')
  {
    stage('Node Install and Test') {
      agent {
        kubernetes {
          label 'nodejs'
       }
      }
      steps {
            checkout scm           
            container('nodejs-container') {
              sh '''
                 yarn install
                 yarn test:unit
                 '''
            }
      } 
    }
    stage('Build image'){
      agent {
        kubernetes{
          label 'kaniko'
        }
      }
      steps {
            checkout scm           
            container(name: 'kaniko-container', shell: '/busybox/sh') {
              sh '''
                 /kaniko/executor --context `pwd` --destination gcr.io/na-csa-msuarez/microblog-from-kaniko:latest
                 '''
            }
      } 
    }
  }
}
