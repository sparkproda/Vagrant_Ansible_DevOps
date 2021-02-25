pipeline {
  agent any
  stages {
    stage ('Build')  {
      agent {
        docker {
          image 'packer_spark:v1'
        }
      }
      steps {
        sh 'ls'
        sh 'packer_spark packer build template.json'

        
      }
    }

  }

}