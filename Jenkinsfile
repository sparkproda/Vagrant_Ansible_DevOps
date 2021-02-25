pipeline {
  agent any
  stages {
    stage ('Build')  {
      agent {
        docker {
          image 'packer_spark:v1'
          args '-v /mnt/packer_data:/data --tmpfs /data'

        }
      }
      steps {
        sh 'ls /data'
        sh 'packer build packer/template.json'

        
      }
    }

  }

}