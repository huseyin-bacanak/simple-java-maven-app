pipeline {
    environment {
        JAVA_TOOL_OPTIONS = '-Duser.home=/var/maven'
    }

    agent {
        docker {
            image 'maven:3-alpine'
            args '-v $HOME/.m2:/var/maven/.m2'
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
        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
