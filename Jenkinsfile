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
    stage('Configure') {
      steps {
        sh '''#!/bin/bash -xe

pwd
printenv | sort
ls -la

# EOF'''
        sh '''#!/bin/bash -xe

MACHINE=udooneo source ./setup-environment build'''
        sh '''ls -la
ls -la conf/'''
      }
    }
  }
}