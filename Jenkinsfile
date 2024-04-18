pipeline {
    agent any
    
    stages{
        stage ('Git Checkout') {
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
    }
}