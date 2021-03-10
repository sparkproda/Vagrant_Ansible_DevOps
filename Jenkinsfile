pipeline {
  agent any
  stages {
    stage ('Build')  {
      agent {
        docker {
          image 'packer_spark:v1'
          args '--dns 8.8.8.8'

        }
      }
      steps {
        sh 'ls /data'
        sh 'packer build packer/template.json'

        
      }
    }

  }

}