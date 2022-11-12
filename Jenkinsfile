pipeline {
  agent any
    stages {
        stage('Pull') {
             steps{
                script{
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                        userRemoteConfigs: [[
                            credentialsId: '123',
                            url: 'https://github.com/Salim-berrima/DevDep.git']]])
                }
            }
          
        } 
      stage('install') {
             steps{
                script{
                    sh " npm install --save-dev @angular-devkit/build-angular"
                }
            }
        }
      
      stage('Build') {
             steps{
                script{
                    sh "ansible-playbook Ansible/build.yml -i Ansible/inventory/host.yml"
                }
            }
        }
  

        stage("Fix the permission issue") {

           

            steps {
                sh "sudo chown root:jenkins /run/docker.sock"
            }

        }
        
        stage('docker') {
             steps{
                script{
                    sh "ansible-playbook Ansible/docker.yml -i Ansible/inventory/host.yml "
                }
            }
        }
        
            
        stage('push docker hub') {
             steps{
                script{
                    sh "ansible-playbook Ansible/docker-registry.yml -i Ansible/inventory/host.yml "
                }
            }
        }
       
    }
   
}
