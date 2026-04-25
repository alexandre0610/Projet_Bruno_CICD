pipeline {
    agent any

    stages {

        stage('Build Docker image') {
            steps {
                sh 'docker build -t playwright-bruno .'
            }
        }

        stage('Run tests in container') {
            agent {
                docker {
                    image 'playwright-bruno'
                    args '-u root --entrypoint=""'
                }
            }

            stages {

                stage('Check Bruno') {
                    steps {
                        sh 'npx @usebruno/cli --version'
                    }
                }

                stage('Run tests') {
                    steps {
                        sh 'npx @usebruno/cli run --env preprod --reporter-html report.html'
                    }
                }
            }
        }
    }
}