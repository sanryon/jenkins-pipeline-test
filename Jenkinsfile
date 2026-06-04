pipeline {
    agent none
    stages {
        stage('Example Build') {
            agent { docker 'maven:3-alpine' }
            steps {
                echo 'Hello, Maven'
                sh 'mvn --version'
            }
        }
        stage('Example Test') {
            agent { docker 'eclipse-temurin:17-jre' }
            steps {
                echo 'Hello, JDK'
                sh 'java -version'
            }
        }
    }
    post {
        success {
            slackSend channel: '#jenkins',
                      color: 'good',
                      message: "✅ 빌드 성공! Job: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
        }
        failure {
            slackSend channel: '#jenkins',
                      color: 'danger',
                      message: "❌ 빌드 실패! Job: ${env.JOB_NAME} #${env.BUILD_NUMBER}"
        }
    }
}
