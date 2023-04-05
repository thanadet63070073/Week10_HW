pipeline {
    agent any
        
        stages {
            stage('Initialize Stage') {
                steps {
                    echo 'Initial : Delete containers and images'
                     dir('Week10_HW') {
                        echo "Current path is  ${pwd()}"
                        sh 'docker-compose down --rmi all --volumes || true'
                     }
                }
            }

            stage('Build Stage'){
                steps {
                    dir('Week10_HW') {
                        echo "Current path is ${pwd()}"
                        sh "docker-compose build"
                    }
                }
            }

            stage('Push to dockerhub Stage'){
                steps {
                    dir('Week10_HW') {
                        withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                            sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                        }
                        sh 'docker push thanadet63070073/frontend_image:1.0'
                        sh 'docker push thanadet63070073/backend_image:1.0'
                    }
                }
            }

            stage('Clear All Container Stage') {
                steps {
                    echo 'Initial : Delete containers and images'
                    sh 'docker stop frontend_server || true'
                    sh 'docker stop backend_server || true'
                    sh 'docker rm frontend_server || true'
                    sh 'docker rm backend_server || true'
                    sh 'docker rmi thanadet63070073/frontend_image:1.0 || true'
                    sh 'docker rmi thanadet63070073/backend_image:1.0 || true'
                }
            }

            stage('Pull Stage') {
                steps {
                    dir('Week10_HW') {
                        echo "Current path is ${pwd()}"
                        sh "docker pull thanadet63070073/frontend_image:1.0"
                        sh "docker pull thanadet63070073/backend_image:1.0"
                    }
                }
            }

            stage('Run Stage') {
                steps {
                    dir('Week10_HW') {
                        echo "Current path is ${pwd()}"
                        sh "docker run -d -p 8081:80 --name frontend_server thanadet63070073/frontend_image:1.0"
                        sh "docker run -d -p 8082:80 --name backend_server  thanadet63070073/backend_image:1.0"
                    }
                }
            }
        }
}