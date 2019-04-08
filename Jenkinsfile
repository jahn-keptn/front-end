@Library('dynatrace@master') _

pipeline {
  agent {
    label 'maven'
  }  
  environment {
    SERVICE_NAME = "front-end"
    VERSION = readFile('version').trim()
    ARTEFACT_ID = "sockshop/" + "${env.SERVICE_NAME}"
    TAG = "${env.DOCKER_REGISTRY_URL}:5000/${env.ARTEFACT_ID}"
    TAG_DEV = "${env.TAG}:${env.VERSION}-${env.BUILD_NUMBER}"
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
      steps {
        container('docker') {
          sh "docker push ${env.TAG_DEV}"
        }
      }
    }
  }
}
