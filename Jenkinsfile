pipeline {
 environment {
    registry = "woualabs07/nodeapp"
    registryCredential = 'Swetha07!'
    dockerImage = ''
  }
    agent any
    stages{
stage('Building image') {
                 steps{
                   script {
                     dockerImage = docker.build registry + ":$BUILD_NUMBER"
                   }
                 }
               }
 stage('Deploy Image') {
                    steps{
                      script {
                        docker.withRegistry( '', registryCredential ) {
                          dockerImage.push()
                        }
                      }
                    }
                  }
    }
}
