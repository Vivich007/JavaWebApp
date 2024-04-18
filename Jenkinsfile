pipeline {
    agent any
    
    stages {
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
        stage ('maven Build') {
            agent {label 'Maven-Ansible'}
            
            steps {
                
                ansiblePlaybook(
                    playbook: '02-MavenConf.yml',
                    inventory:'Hosts.ini'
                )
            }    
        }    

    }
}