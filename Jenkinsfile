pipeline {
  agent any
    stages {
        stage('git Pull') {
             steps{
                script{
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                        userRemoteConfigs: [[
                            credentialsId: '****',
                            url: 'https://github.com/Salim-berrima/DevDep.git']]])
                }
            }
          
        } 
      stage('npm install') {
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
  

     
        
        stage('build docker & run container') {
             steps{
                script{
                    sh "ansible-playbook Ansible/docker.yml -i Ansible/inventory/host.yml "
                }
            }
        }
        
            
        stage('push to docker hub') {
             steps{
                script{
                    sh "ansible-playbook Ansible/docker-registry.yml -i Ansible/inventory/host.yml "
                }
            }
        }
       
    }
   
}
