pipeline {
    agent {
        docker {
            image 'ruby:3.3'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'gem install bundler'
                sh 'bundle install'
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
            echo 'Pipeline done'
        }
        success {
            echo 'SUCCESS!'
        }
        failure {
            echo '❌ FAILURE!'
        }
    }
}