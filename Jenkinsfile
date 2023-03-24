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
            script {
                def jsonFile = readFile 'report.json'
                def jsonData = readJSON text: jsonFile
                sh "echo ${jsonData}"
                sh "echo ${jsonData.created_pull_request[0].repo}"
                //sh "Repo: ${jsonData.created_pull_request[0].repo}"
                //echo "Message: ${jsonData.created_pull_request[0].msg}"
                
                def report = readFile 'report_2'
                sendSlackMessage(msg: ${report})
            }

            //echo "Repo: ${jsonData.created_pull_request[0].repo}"
            //echo "Message: ${jsonData.created_pull_request[0].msg}"
            //sendSlackMessage(msg: "${jsonData.created_pull_request[0].repo}")
            sendSlackMessage()
        }
    }
}
