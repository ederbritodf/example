 pipeline {
  environment {
      registry = "nexus"
      dockerRegistry = "172.18.0.7"
      registryCredential = 'admin'
      ImageName = "example"
      ImageTag= "01"
      dockerImage = ''
      gitRepositoryUrl = "https://github.com/ederbritodf/example.git"
      gitCredential = "ederbritodf"
      gitBranch = "master"
  }

agent any

stages { 
      stage('Building image') {
        steps{
          script {
            dockerImage = docker.build registry + "/$ImageName:$ImageTag"
          }
        }
      }
      stage('Deploy Image') {
        steps{
          script {
              docker.withRegistry( '$dockerRegistry', 'docker-registry' ) {
                  docker.build(ImageName)
                      .push(ImageTag)
            }
          }
        }
      }
      /*stage('Remove Unused docker image') {
        steps{
         sh "echo removed"
         
          sh "docker rmi $registry/$ImageName:$ImageTag"
          
        }
      }*/
    }
  }
