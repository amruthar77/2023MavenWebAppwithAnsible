pipeline {
    agent any  // Use any available agent
    
    environment {
        LANG = 'en_US.UTF-8'
        LC_ALL = 'en_US.UTF-8'
    }   // this has to be added only if you get an error saying UTF required is 8 but showing in ISO00009

    tools {
        maven 'Maven'  // Ensure this matches the name configured in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/amruthar77/2023MavenWebAppwithAnsible.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'  // Run Maven build
            }
        }

     stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint:true
            }
        }
       stage('Deploy') {
    steps {
        // No need to run 'mvn clean package' again here; it was done in the Build stage!
        
        // If you have configured passwordless sudo for the jenkins user:
        sh 'ansible-playbook playbook.yml -i hosts.ini' 
        
        // OR, if you use the Ansible Plugin (recommended):
        /*
        ansiblePlaybook(
            playbook: 'playbook.yml',
            inventory: 'hosts.ini',
            sudoUser: 'root'
        )
        */
    }
}
                  
    }

   }
