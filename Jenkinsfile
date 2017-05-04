pipeline {
  agent {
    docker {
      image 'gmacario/build-yocto:latest'
    }
    
  }
  stages {
    stage('Checkout') {
      steps {
        ws(dir: 'fsl') {
          echo 'INFO: Checkout'
          sh '''#!/bin/bash -xe

id
pwd
ls -la

# EOF'''
          sh '''#!/bin/bash -xe

# CONFIGURABLE OPTIONS
#
REPO_URL=https://github.com/graugans/fsl-community-bsp-platform
#
# REPO_BRANCH=master-next
# REPO_BRANCH=morty
# REPO_BRANCH=krogoth
REPO_BRANCH=jethro

repo init -u ${REPO_URL} -b ${REPO_BRANCH}

# EOF'''
          sh '''#!/bin/bash -xe

repo sync

# DEBUG
repo manifest -r

# EOF'''
        }
        
      }
    }
    stage('Configure') {
      steps {
        ws(dir: 'fsl') {
          echo 'INFO: Configuring build'
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

# Uncomment for a scratch build
# rm -rf build/

# Workaround for "Please use a locale setting which supports utf-8."
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
export LANGUAGE=en_US.UTF-8 

# Silence accepting Freescale EULA
export EULA=1

# ./setup-environment --help

MACHINE=udooneo DISTRO=poky source ./setup-environment build

# Add extra Yocto layers
echo 'BBLAYERS += "   ${BSPDIR}/sources/meta-udoo "' >>conf/bblayers.conf

# DEBUG
ls -la
ls -la conf/ || true
cat conf/bblayers.conf || true
cat conf/local.conf || true

# EOF'''
        }
        
      }
    }
    stage('Build') {
      steps {
        ws(dir: 'fsl') {
          echo 'INFO: Building'
          sh '''#!/bin/bash -xe

# Workaround for "Please use a locale setting which supports utf-8."
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
export LANGUAGE=en_US.UTF-8 

source ./setup-environment build

# DEBUG
cat conf/local.conf
cat conf/bblayers.conf

# bitbake logrotate
bitbake core-image-minimal
# bitbake core-image-full-cmdline

# EOF'''
        }

        sh '''#!/bin/bash -xe

# DEBUG
pwd
ls -la
ls -la build/
ls -la build/tmp/
ls -la build/tmp/deploy/
ls -la build/tmp/deploy/images/
ls -la build/tmp/deploy/images/udooneo/

# EOF'''

        // Archive the build output artifacts
        archive includes: 'build/tmp/deploy/images/*/*.sdcard.gz'
      }
    }
  }
}
