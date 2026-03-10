pipeline {
    agent any

    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }

    stages {

        stage('Clone Repo') {
            steps {
                git branch: 'main', url: 'https://github.com/ZaidMohammad38/jenkins-docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t zaidmohammad038/static-web .'
            }
        }

        stage('Docker Login') {
            steps {
                sh 'docker login -u zaidmohammad038 -p YOUR_PASSWORD'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push zaidmohammad038/static-web'
            }
        }

        stage('Deploy using Ansible') {
            steps {
                sh 'ansible-playbook -i inventory playbook.yml'
            }
        }

    }
}
