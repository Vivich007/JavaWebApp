pipeline {
    agent any
    
    stages {
       
        stage ('Install Packages') {
            agent {label 'n150'}
            steps {
                echo 'Install required packages'
                ansiblePlaybook(
                    playbook: '01-Install.yml',
                    inventory: 'Hosts.ini'
                )
                
            }    
        }   
        stage ('Maven Build') {
            agent {label 'n150'}
            steps {
                echo 'Build Maven Package'
                ansiblePlaybook(
                    playbook: '02-Build.yml',
                    inventory: 'Hosts.ini'
                )
            }    
        }   

         stage ('Build Test') {
            agent {label 'n150'}
            steps {
                echo 'Test Maven Build'
                ansiblePlaybook(
                    playbook: '03-Test.yml',
                    inventory: 'Hosts.ini'
                )  
            }    
        }    

        stage ('Deploy') {
            agent {label 'n150'}
            
            steps {
                echo 'Deploy WAR files'
                ansiblePlaybook(
                    playbook: '04-Deploy.yml',
                    inventory: 'Hosts.ini'
                )
            }    
        }    
    }

    post {
        always {
            echo 'Send email notification'
            emailext (
                to: 'vivich007@gmail.com',
                subject: "${currentBuild.fullDisplayName}",
                body: "Check Build Job."
            )    
        }
    }   
}