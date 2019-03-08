@Library('dynatrace@master') _

pipeline {
  agent {
    label 'maven'
  }
  environment {
    APP_NAME = "catalog"
    ARTEFACT_ID = "kube-demo/" + "${env.APP_NAME}"
    VERSION = readFile('version').trim()
    TAG = "${env.DOCKER_REGISTRY_URL}:5000/library/${env.ARTEFACT_ID}"
    TAG_DEV = "${env.TAG}-${env.VERSION}-${env.BUILD_NUMBER}"
    TAG_STAGING = "${env.TAG}-${env.VERSION}"
  }
  stages {
    stage('Docker build') {
      steps {
        container('docker') {
          sh "docker build -t ${env.TAG_DEV} ."
        }
      }
    }
    stage('Docker push to registry'){
      }
      steps {
        container('docker') {
          sh "docker push ${env.TAG_DEV}"
        }
      }
    }
  }
}
