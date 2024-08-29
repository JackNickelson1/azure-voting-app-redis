pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello'
            }
        }

        stage('Bye') {
            steps {
                echo 'Bye'
            }
        }

        stage('Docker build') {
            steps {
                pwsh(script: 'docker images -a')
            }
        }
    }
}