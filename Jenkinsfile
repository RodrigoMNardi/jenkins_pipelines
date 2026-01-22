pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "ruby-rspec-tests"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Run Unit Tests') {
            steps {
                script {
                    docker.image("${DOCKER_IMAGE}").inside {
                        sh 'bundle exec rspec'
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finalizada'
        }
        success {
            echo '✅ Testes passaram com sucesso'
        }
        failure {
            echo '❌ Falha nos testes'
        }
    }
}