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
rm -rf build/

export EULA=1

# ./setup-environment --help

MACHINE=udooneo source ./setup-environment build

# Add extra Yocto layers
cat >>conf/bblayers.conf <<END
BBLAYERS += "   \${BSPDIR}/sources/meta-udoo "
END

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

MACHINE=udooneo source ./setup-environment build

# DEBUG
cat conf/local.conf
cat conf/bblayers.conf

bitbake core-image-minimal

# EOF'''
      }
    }
  }
}