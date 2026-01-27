pipeline {
    agent none

    stages {
        stage('Checkout') {
            agent {
                docker {
                    image 'ruby:3.4'
                }
            }
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
            agent {
                docker {
                    image 'ruby:3.4'
                }
            }
            steps {
                sh 'gem install bundler -v 2.7.1'
            }
        }

        stage('Install gems') {
            agent {
                docker {
                    image 'ruby:3.4'
                }
            }
            steps {
                sh 'bundle install'
            }
        }

        stage('Unit Tests') {
            agent {
                docker {
                    image 'ruby:3.4'
                }
            }

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
