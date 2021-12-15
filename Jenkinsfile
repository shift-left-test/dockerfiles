pipeline {
    agent any
    stages {
        stage("yocto-dev-18.04") {
            environment {
                NAME = "test-image-${new Random().nextInt(123456789)}"
            }
            steps {
                sh 'docker build -f yocto-dev/18.04/Dockerfile -t $NAME .'
            }
            post {
                always {
                    sh 'docker rmi -f $NAME'
                }
            }
        }
        stage("yocto-dev-16.04") {
            environment {
                NAME = "test-image-${new Random().nextInt(123456789)}"
            }
            steps {
                sh 'docker build -f yocto-dev/16.04/Dockerfile -t $NAME .'
            }
            post {
                always {
                    sh 'docker rmi -f $NAME'
                }
            }
        }
        stage("jenkins-dev") {
            environment {
                NAME = "test-image-${new Random().nextInt(123456789)}"
            }
            steps {
                sh 'docker build -f jenkins-dev/Dockerfile -t $NAME .'
            }
            post {
                always {
                    sh 'docker rmi -f $NAME'
                }
            }
        }
        stage("ubuntu-dev") {
            environment {
                NAME = "test-image-${new Random().nextInt(123456789)}"
            }
            steps {
                sh 'docker build -f ubuntu-dev/Dockerfile -t $NAME .'
            }
            post {
                always {
                    sh 'docker rmi -f $NAME'
                }
            }
        }
        stage("clang-dev-11") {
            environment {
                NAME = "test-image-${new Random().nextInt(123456789)}"
            }
            steps {
                sh 'docker build -f clang-dev/11/Dockerfile -t $NAME .'
            }
            post {
                always {
                    sh 'docker rmi -f $NAME'
                }
            }
        }
        stage("clang-dev-9") {
            environment {
                NAME = "test-image-${new Random().nextInt(123456789)}"
            }
            steps {
                sh 'docker build -f clang-dev/9/Dockerfile -t $NAME .'
            }
            post {
                always {
                    sh 'docker rmi -f $NAME'
                }
            }
        }
    }
}
