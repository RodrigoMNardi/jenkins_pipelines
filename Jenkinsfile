pipeline {
    agent {
        dockerfile {
            filename 'dockerfiles/ruby34/Dockerfile'
            label ''
            additionalBuildArgs ''
        }
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'bundle exec rspec'
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