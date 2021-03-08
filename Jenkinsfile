pipeline {
  agent { label 'docker&&jenkins-slave&&qa' }
  environment {
    // Variable for an example.
    SUPERLOOP_ENV = 'qa'
  }
  stages {
    stage('Checkout Git'){
      steps {
        // This checks out the repo with the current jenkisnfile
        checkout scm

        // This checks out an arbitrary git URL
        dir('superloop') {
            git url: 'https://gerrit.corp.skytap.com/infra/networking/superloop'
        }
        dir('superloop_cfgs') {
            // URL with a variable
            git url: 'https://gerrit.corp.skytap.com/infra/networking/superloop_cfgs_${SUPERLOOP_ENV}'
        }
      }
    }

    stage('Environment Setup') {
      steps {
        sh('ls superloop')
        sh('ls superloop_cfgs')
      }
    }
  }
}
