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
    }
}
