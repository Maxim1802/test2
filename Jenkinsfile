@Library("explorer-jenkins-lib") _

pipeline {
    agent {
        node {
            label 'aws-ec2-docker'
        }
    }
    stages {
        stage('Send notify') {
            agent any
            steps {
                sendSlackMessage()
                setBuildStatus()
            }
        }
        stage('Npm install') {
            agent { 
              docker {
                image 'python:3.7.16-slim-bullseye' 
                reuseNode true
                args  '--entrypoint="" -u root'
              }
            }
            steps {
              sh 'ls'              
            }
        }
    }
    post {
        always {
            sendSlackMessage(msg: "test")
        }
    }
}
