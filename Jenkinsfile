pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checkout Stage'
            }
        }

        stage('Validate') {
            steps {
                echo 'Validating Infrastructure Files'
            }
        }

        stage('Ansible') {
            steps {
                echo 'Ansible Stage'
            }
        }

        stage('AMI Bake') {
            steps {
                echo 'AMI Bake Stage'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy Stage'
            }
        }
    }
}