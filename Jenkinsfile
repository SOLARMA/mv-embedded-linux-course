pipeline {
  agent {
    docker {
      image 'gmacario/build-yocto:latest'
    }
    
  }
  stages {
    stage('Checkout') {
      steps {
        echo 'INFO: Checkout'
        sh '''#!/bin/bash -xe

id
pwd
ls -la

# EOF'''
        sh '''#!/bin/bash -xe

repo init     -u https://github.com/graugans/fsl-community-bsp-platform     -b jethro

# EOF'''
        sh '''#!/bin/bash -xe

# DEBUG
repo manifest -r

repo sync

# EOF'''
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
ls -la sources/ || true

# DEBUG
cat build/conf/bblayers.conf || true
cat build/conf/local.conf || true

export ACCEPT_FSL_EULA="1"
export MACHINE=udooneo
source ./setup-environment build

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