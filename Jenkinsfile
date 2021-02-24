pipeline {
  agent {
    docker {
      image 'packer_terraform_docker:v1'
    }
  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

  }

}