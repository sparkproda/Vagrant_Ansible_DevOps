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
        sh 'ls ./packer'
        sh 'cd packer'
        sh 'packer build template.json'

        
      }
    }

  }

}