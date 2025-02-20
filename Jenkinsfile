pipeline {
    agent any

    triggers {
        cron('H/3 * * * 4') // Runs every 3 minutes on Thursdays
    }

    tools {
        maven 'maven3'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'git@github.com:Maxafangsco/midtermexam.git'
            }
        }

        stage('Build and Test') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Generate Jacoco Coverage Report') {
            steps {
                sh 'mvn test jacoco:report'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'target/site/jacoco/index.html', fingerprint: true
                }
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}