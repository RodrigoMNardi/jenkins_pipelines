pipeline {
    agent none

    stages {
        stage('Checkout') {
            agent any
            steps {
                deleteDir()
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: 'master']],
                    userRemoteConfigs: [[url: 'https://github.com/RodrigoMNardi/netdef-ci-github-app.git']]
                ])
            }
        }

        stage('Install and Test') {
            agent {
                docker {
                    image 'ruby:3.4'
                }
            }
            stage('Install bundler and dependencies') {
              steps {
                  sh 'gem install bundler'
                  sh 'bundle install'
              }
            }

            stage('Unit Tests') {
              steps {
                  sh 'bundle exec rspec'
              }
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
