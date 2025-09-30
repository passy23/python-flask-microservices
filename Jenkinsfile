pipeline {
    agent any

    parameters {
        string(name: 'IMAGE_NAME', defaultValue: 'frontend', description: 'this the name of my docker image for frontend application')
        string(name: 'IMAGE_TAG', defaultValue: 'latest', description: '')
        string(name: 'GITHUB_USER', defaultValue: 'passy23', description: '')
        string(name: 'CONTAINER_NAME', defaultValue: 'frontendapp', description: '')
        string(name: 'DOCKER_HUB_USER', defaultValue: 'pascaline2019', description: '')
        
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
                        docker rm -f frontendapp
                        echo "Launch test container"
                        docker run -d -p 5000:5000 --name ${CONTAINER_NAME} ${IMAGE_NAME}:${IMAGE_TAG}
                        sleep 5
                        echo "test container"
                        curl -I http://$(docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' ${CONTAINER_NAME}):5000
                        echo "delete the conatiner"
                        docker rm -f ${CONTAINER_NAME}

                    '''
                }
            }
        }


        stage ('Push Image') {
            steps {
                script {
                    withCredentials([usernamePassword(
                        credentialsId: 'githup-credentials', 
                        passwordVariable: 'DOCKER_PASSWORD', 
                        usernameVariable: 'DOCKER_USER'
                        
                        )]) {
                            sh '''
                                docker tag ${IMAGE_NAME}:${IMAGE_TAG} ${DOCKER_HUB_USER}/${IMAGE_NAME}:${IMAGE_TAG}
                                docker login -u $DOCKER_USER -p $DOCKER_PASSWORD
                                docker push ${DOCKER_HUB_USER}/${IMAGE_NAME}:${IMAGE_TAG}
                            '''

                        }
                    
                }
            }
        }

    
    }
}