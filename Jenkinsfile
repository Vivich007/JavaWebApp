pipeline {
    agent any
    
    stages {
        
        stage ('Install Packages') {
            
            
            steps {
                echo 'Install required packages'
                ansiblePlaybook credentialsId: 'Ansible-Project', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'Hosts.ini', playbook: '01-Install.yml', vaultTmpPath: ''
                
            }    
        }   
        stage ('Maven Build') {
            
            
            steps {
                ansiblePlaybook credentialsId: 'Ansible-Project', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'Hosts.ini', playbook: '02-Build.yml', vaultTmpPath: ''
                
            }    
        }   

         stage ('Build Test') {
            
            
            steps {
                ansiblePlaybook credentialsId: 'Ansible-Project', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'Hosts.ini', playbook: '03-Test.yml', vaultTmpPath: ''
                
            }    
        }    

        stage ('Deploy') {
            
            
            steps {
                echo 'Deploy War file to Servers'
                ansiblePlaybook credentialsId: 'Ansible-Project', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'Hosts.ini', playbook: '05-Deploy.yml', vaultTmpPath: ''
                
            }    
        }    
    }

    post {
        always {
            echo 'Send email notification'
            emailext (
                to: 'vivich007@gmail.com',
                subject: "Failed: ${currentBuild.fullDisplayName}",
                body: "you tried abeg! e no easy."
            )    
        }
    }   
}