pipeline {
    agent any

    environment {
        DOCKER_NS = "${DOCKER_REGISTRY}/twbc"
        DOCKER_HUB_USERNAME = 'AWS'
        DOCKER_HUB_PASSWORD = sh(script: 'aws ecr get-login-password', returnStdout: true)
    }

    stages {
        stage('build & push image') {
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
}
