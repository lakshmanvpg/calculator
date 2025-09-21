pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK'
    }

    environment {
        DEPLOY_PATH = "D:\\maven_practice"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/lakshmanvpg/calculator.git'
            }
        }

        stage('Build') {
            steps { bat "mvn clean install" }
        }

        stage('Test') {
            steps { bat "mvn test" }
        }

        stage('Package') {
            steps { bat "mvn package" }
        }

        stage('Archive Artifacts') {
            steps { archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true }
        }

        stage('Deploy') {
            steps {
                bat "if not exist \"%DEPLOY_PATH%\" mkdir \"%DEPLOY_PATH%\""
                bat "copy /Y target\\*.jar \"%DEPLOY_PATH%\""
            }
        }
    }

    post {
        success { echo "Build and deployment completed " }
        failure { echo "Build or deployment failed " }
    }
}
