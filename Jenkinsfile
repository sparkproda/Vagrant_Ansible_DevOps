pipeline {
  agent {
    docker {
      image 'packer_spark:v1'
    }
  }
  stages {
    stage('Build') {
      steps {
        sh 'packer_spark packer build template.json'
      }
    }

  }

}