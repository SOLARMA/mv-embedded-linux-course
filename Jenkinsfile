pipeline {
  agent {
    docker {
      image 'gmacario/build-yocto:latest'
    }
    
  }
  stages {
    stage('Checkout') {
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
    stage('Verify') {
      steps {
        sh '''#!/bin/bash -xe

pwd
printenv | sort
ls -la

# EOF'''
      }
    }
  }
}