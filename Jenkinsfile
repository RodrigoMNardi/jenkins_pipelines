pipeline {
    agent {
        docker {
            image 'ruby:3.4'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install bundler') {
            steps {
                sh 'gem install bundler'
            }
         }

        stage('Install dependencies') {
            steps {
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