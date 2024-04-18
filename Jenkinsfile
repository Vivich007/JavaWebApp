pipeline {
    agent any
    
    stages {
        stage ('') {
            steps {
                git repository
            }
        }

        stage ('Install Packages') {
            agent {label 'Maven-Ansible'}
            
            steps {
                echo 'Install required packages'
                ansiblePlaybook credentialsId: 'Ansible-Project', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'Hosts.ini', playbook: '01-Install.yml', vaultTmpPath: ''
                
            }    
        }   
        stage ('Maven Build') {
            agent {label 'Maven-Ansible'}
            
            steps {
                ansiblePlaybook credentialsId: 'Ansible-Project', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'Hosts.ini', playbook: '02-Build.yml', vaultTmpPath: ''
                
            }    
        }   

         stage ('Build Test') {
            agent {label 'Maven-Ansible'}
            
            steps {
                ansiblePlaybook credentialsId: 'Ansible-Project', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'Hosts.ini', playbook: '03-Test.yml', vaultTmpPath: ''
                
            }    
        }    

        stage ('Deploy') {
            agent {label 'Maven-Ansible'}
            
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