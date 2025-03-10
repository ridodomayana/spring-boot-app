pipeline {
    agent any
    tools {
        jdk 'java17'
        maven 'maven'
    }
    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_Access_Key')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_Secret_Key')
        S3_BUCKET = 'demo-bucket-03-09-2025-new'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ridodomayana/spring-boot-app.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Upload Artifact to S3') {
            steps {
                script {
                    def artifact = sh(script: "find -name '*.war'", returnStdout: true).trim()
                    sh "aws s3 cp ${artifact} s3://${S3_BUCKET}/"
                }
            }
        }
    }
}
