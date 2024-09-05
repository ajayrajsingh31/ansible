pipeline {
    agent any
    tools {
        ansible 'ansible'
    }
    stages {
        stage('cleanws') {
            steps {
                cleanWs()
            }
        }
        stage('checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ajayrajsingh31/ansible.git'
            }
        }
        stage('Setup Virtual Environment') {
            steps {
                sh 'python3 -m venv venv'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh '''
                . venv/bin/activate
                pip install --upgrade requests==2.20.1
                '''
            }
        }
        stage('ansible provision') {
            steps {
                sh '''
                . venv/bin/activate
                ansible-playbook ec2.yaml
                '''
            }
        }
    }
}
