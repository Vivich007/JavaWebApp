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
                ansiblePlaybook(
                    playbook: '01-Install.yml',
                    inventory:'Hosts.ini'
                )
        }    
    }
}