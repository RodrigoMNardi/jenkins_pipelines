pipeline {
    agent {
        docker {
            image 'ruby:3.4'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                deleteDir()
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: 'master']],
                    userRemoteConfigs: [[url: 'https://github.com/RodrigoMNardi/netdef-ci-github-app.git']]
                ])
            }
        }

        stage('Install bundler') {
            steps {
                sh 'gem install bundler -v 2.7.1'
            }
        }

        stage('Install gems') {
            steps {
                sh 'bundle install'
            }
        }

        stage('Unit Tests') {
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
