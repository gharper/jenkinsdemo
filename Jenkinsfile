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
        sh('ssh -oStrictHostKeyChecking=no jenkins@gerrit.corp.skytap.com -p 29418 || true')
        // This checks out an arbitrary git URL
        dir('superloop') {
            git branch: 'master',
                credentialsId: '7a2a7ec4-f126-4f50-916d-db89c7f55089',
                url: 'ssh://jenkins@gerrit.corp.skytap.com:29418/infra/networking/superloop'
        }
        dir('superloop_cfgs') {
            // URL with a variable
            git branch: 'master',
                credentialsId: '7a2a7ec4-f126-4f50-916d-db89c7f55089',
                url: 'ssh://jenkins@gerrit.corp.skytap.com:29418/infra/networking/superloop_cfgs_${SUPERLOOP_ENV}'
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
