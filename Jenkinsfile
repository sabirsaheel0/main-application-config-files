pipeline {
    agent any
    parameters {
        string(name: 'IMAGE_TAG', description: 'ENTER THE IMAGE TAG!')
    }

    stages {
        stage('Update Image Tag') {
            steps {
                sh 'cat ./k8s/deployment.yaml'
                sh "sed -i 's/jenkinstest.*/jenkinstest:${IMAGE_TAG}/g' ./k8s/deployment.yaml"
                sh 'cat ./k8s/deployment.yaml'
            }
        }
        stage('Push to github') {
            steps {
                sh 'git config --global user.email sabirsaheel17@gmail.com'
                sh 'git config --global user.name sabirsaheel0'
                sh 'git add ./k8s/deployment.yaml'
                sh "git commit -m'updated image tag to ${IMAGE_TAG}'"
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'password', usernameVariable: 'username')]) {
                    sh "git push https://${username}:${password}@github.com/sabirsaheel0/main-application-config-files.git main"
                }
            }
        }
    }
}