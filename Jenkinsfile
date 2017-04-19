pipeline {
  agent {
    docker {
      image 'gmacario/build-yocto:latest'
    }
    
  }
  stages {
    stage('Stage 1') {
      steps {
        echo 'Stage 1'
        sh '''#!/bin/sh

id
pwd
ls -la

# EOF'''
        sh 'repo init -u https://github.com/graugans/fsl-community-bsp-platform -b jethro'
        sh 'repo sync'
      }
    }
  }
}