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
  }
}
