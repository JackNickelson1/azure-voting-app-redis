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
                bat(script: 'docker images -a')
                bat(script: """
                    cd azure-vote/
                    docker images -a
                    docker build -t jenkins-pipeline .
                    docker images -a
                    cd ..
                """)
            }
        }
    }
}