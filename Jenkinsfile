pipeline {
    agent any
    parameters {
        string(name: 'IMAGE_TAG', description: 'ENTER THE IMAGE TAG!')
    }

    stages {
        stage('Update Image Tag') {
            steps {
                cat ./k8s/deployment.yaml
                sh "sed -i 's/jenkinstest.*/jenkinstest:${IMAGE_TAG}/g ./k8s/deployment.yaml"
            }
        }
    }
}