pipeline {
    agent any

    environment {
        DOCKER_NS = "twblockchain"
        VERSION = "0.4.22-gm-build-${BUILD_NUMBER}"
    }

    stages {
        stage('prepare') {
            steps {
                sh '''
                make clean
                '''
            }
        }

        stage('build docker') {
            steps {
                sh '''
                make docker
                '''
            }
        }

        stage('push image') {
            parallel {
                stage('baseos') {
                    steps {
                        sh '''
                        make build/docker/baseos/.push
                        '''
                    }
                }

                stage('baseimage') {
                    steps {
                        sh '''
                        make build/docker/baseimage/.push
                        '''
                    }
                }
            }
        }
    }
}
