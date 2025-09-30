pipeline {
    agent any

    parameters {
        string(name: 'IMAGE_NAME', defaultValue: 'frontent', description: 'this the name of my docker image for frontend application')
        string(name: 'IMAGE_TAG', defaultValue: 'latest', description: '')
        string(name: 'GITHUP_USER', defaultValue: 'passy23', description: '')
        string(name: 'CONTENER_NAME', defaultValue: 'frontendapp', description: '')
        
    }

    stages {
        stage ('Build Image'){
          steps {
              script {
                sh 'docker build -t ${IMAGE_NAME}:${IMAGE_TAG} frontend/'
            }
          }
        }
    }
}