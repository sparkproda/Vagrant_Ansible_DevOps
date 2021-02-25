pipeline {
  agent any
  stages {
    stage ('Build')  {
      agent {
        docker {
          image 'packer_spark:v1'
          args '-u root:root'

        }
      }
      steps {
        sh 'ls /data'
        sh 'packer build packer/template.json'

        
      }
    }

  }

}