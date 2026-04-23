pipeline {
    agent any  

    environment {
        LANG = 'en_US.UTF-8'
        LC_ALL = 'en_US.UTF-8'
    }

    tools {
        maven 'Maven'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/amruthar77/2023MavenWebAppwithAnsible.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Verify WAR') {
            steps {
                sh 'ls -l target/'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                ansible-playbook playbook.yml -i hosts.ini
                '''
            }
        }
    }

    post {
        success {
            echo 'Deployment successful '
        }
        failure {
            echo 'Deployment failed '
        }
        always {
            cleanWs()
        }
    }
}
