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

# DEBUG
pwd
ls -la
ls -la build/ || true
ls -la build/conf/ || true
cat build/conf/bblayers.conf || true
cat build/conf/local.conf || true

MACHINE=udooneo source ./setup-environment build

# DEBUG
ls -la
ls -la conf/ || true
cat conf/bblayers.conf || true
cat conf/local.conf || true

# EOF'''
      }
    }
  }
}