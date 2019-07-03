DOCKER_MAVEN_IMAGE = 'maven:3.5.2-jdk-8-alpine'
DOCKER_MAVEN_ARGS = '-v $HOME/.m2:/root/.m2'

pipeline {
    agent {
        docker {
            image DOCKER_MAVEN_IMAGE
            args DOCKER_MAVEN_ARGS
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }

            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
    }

}
