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

        stage ('Test Image') {
            steps {
                script {
                    sh '''
                        echo "Launch test container"
                        docker run -d -p 5000:5000 --name ${CONTENER_NAME} ${IMAGE_NAME}:${IMAGE_TAG}
                        sleep 5
                        echo "test container"
                        curl -I http://$(docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ${CONTAINER_NAME}):5000
                        echo "delete the conatiner"
                        docker rm -f ${CONTENER_NAME}

                    '''
                }
            }
        }

    
    }
}