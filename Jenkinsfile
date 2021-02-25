pipeline {
  agent any
  stages {
    stage ('Build')  {
      agent {
        docker {
          image 'packer_spark:v1'
          args '--tmpfs /data'

        }
      }
      steps {
        sh 'ls /data'
        sh 'packer build packer/template.json'

        
      }
    }

  }

}