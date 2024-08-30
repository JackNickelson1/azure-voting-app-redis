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

        stage('Start test app') {
            steps {
                bat(script: """
                    docker-compose up -d
                """)
            }
        }

        stage('Stop app') {
            steps {
                bat(script: """
                    docker-compose down
                """)
            }
        }

        stage('Push container') {
            steps {
                echo "Workspace is $WORKSPACE"
                dir("$WORKSPACE/azure-vote") {
                    script {
                        docker.withRegistry('https://index.docker.io/v1/', 'DockerHubCredentials')
                        def image = docker.build('stevendube/jenkins-pipeline:latest')
                        image.push()
                    }
                }
            }
        }
    }
}