 pipeline {
  environment {
      registry = "nexus"
      dockerRegistry = "http://172.18.0.7:5001"
      ImageName = "example"
      ImageTag= '${env.BUILD_ID}'
      dockerImage = ''
      gitRepositoryUrl = "https://github.com/ederbritodf/example.git"
      gitCredential = "ederbritodf"
      gitBranch = "master"
  }

agent any

stages { 
      stage('Build Image') {
        steps{
          script {
            dockerImage = docker.build registry + "/$ImageName:$ImageTag"
          }
        }
      }
      stage('Deploy Image Registry') {
        steps{
          script {
              docker.withRegistry('http://172.18.0.7:5001' , 'docker-registry' ) {
                  docker.build(ImageName)
                      .push(ImageTag)
            }
          }
        }
      }
      stage('Clean Workspace') {
        steps{
         sh "docker rmi -f 172.18.0.7:5001/$ImageName:$ImageTag"
        }
      }
    }
  }
