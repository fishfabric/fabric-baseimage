pipeline {
    agent any

    environment {
        DOCKER_NS = "${DOCKER_REGISTRY}/twbc"
    }

    stages {
        stage('build & push image') {
            parallel {
                stage('baseos') {
                    steps {
                        sh '''
                        aws ecr get-login-password | docker login --username AWS --password-stdin ${DOCKER_REGISTRY}
                        make build/docker/baseos/.push
                        '''
                    }
                }

                stage('baseimage') {
                    steps {
                        steps {
                            sh '''
                            aws ecr get-login-password | docker login --username AWS --password-stdin ${DOCKER_REGISTRY}
                            make build/docker/baseimage/.push
                            '''
                        }
                    }
                }
            }
        }
    }
}
