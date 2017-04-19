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

repo init -u https://github.com/graugans/fsl-community-bsp-platform     -b jethro

# EOF'''
        sh '''#!/bin/bash -xe

repo sync

# DEBUG
repo manifest -r

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

# FIXME: Should not append if already present
[ -e build/conf/local.conf ] && cat >>build/conf/local.conf <<END
ACCEPT_FSL_EULA="1"
END

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
    stage('Build') {
      steps {
        sh '''#!/bin/bash -xe

# DEBUG
pwd
ls -la
ls -la build/ || true
ls -la build/conf/ || true
ls -la sources/ || true

./setup-environment --help

MACHINE=udooneo source ./setup-environment build
MACHINE=udooneo bitbake core-image-minimal

# EOF'''
      }
    }
  }
}