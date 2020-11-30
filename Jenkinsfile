pipeline {
    agent any

    environment {
        DOCKER_NS = "${DOCKER_REGISTRY}/twbc"
        VERSION = "0.4.22-gm-build-${BUILD_NUMBER}"
    }

    stages {
        stage('prepare') {
            steps {
                sh '''
                make clean
                aws ecr get-login-password | docker login --username AWS --password-stdin ${DOCKER_REGISTRY}
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
