pipeline {

    agent any

    stages {
        stage("building") {
            steps {
                sshagent(['nodessh']) {
                    sh """
                        ssh -o StrictHostKeyChecking=no ubuntu@52.53.251.73 << EOF
                        git clone https://github.com/mayank2815794/devops-task.git
                        cd devops-task
                        docker build -t mayankpatil/node-web-app:${BUILD_NUMBER} .
                        exit 0
                        << EOF
                    """
                }
            }
        }
        stage("Deploy") {
            steps {
                sshagent(['nodessh']) {
                    sh """
                        ssh -o StrictHostKeyChecking=no ubuntu@52.53.251.73 << EOF
                        docker run --name nodeapp-${BUILD_NUMBER} -p 8080 -d mayankpatil/node-web-app:${BUILD_NUMBER}
                        docker ps | grep nodeapp-${BUILD_NUMBER}
                        exit 0
                        << EOF
                    """
                }
            }
        }
    }
}
