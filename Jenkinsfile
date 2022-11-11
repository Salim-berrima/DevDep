pipeline {
  agent any
    stages {
        stage('Pull') {
             steps{
                script{
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                        userRemoteConfigs: [[
                            credentialsId: '123',
                            url: 'https://github.com/Salim-berrima/DevOps-Deploy.git']]])
                }
            }
        }
    }
}
