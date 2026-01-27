pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build and Test in Docker') {
            steps {
                script {
                    def app = docker.build('ruby34-test', 'dockerfiles/ruby34')
                    app.inside {
                        sh 'bundle install'
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