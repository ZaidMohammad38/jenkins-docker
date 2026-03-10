pipeline {
    agent any

    stages {

        stage('Clone Repo') {
            steps {
                git 'https://github.com/yourusername/project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t yourdockerhub/static-web .'
            }
        }

        stage('Docker Login') {
            steps {
                sh 'docker login -u yourdockerhub -p yourpassword'
            }
        }

        stage('Push Image') {
            steps {
                sh 'docker push yourdockerhub/static-web'
            }
        }

        stage('Deploy with Ansible') {
            steps {
                sh 'ansible-playbook -i inventory playbook.yml'
            }
        }

    }
}
