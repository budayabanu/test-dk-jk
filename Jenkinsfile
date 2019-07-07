pipeline {
    agent none
    stages {
        stage ("Docker image build and push") {
            stages {
                stage('AWS Login') {
                      steps {
                        script {
                            sh 'eval $(aws ecr get-login --no-include-email --region  eu-west-1)'
                        }
                      }
                }
                stage("Docker build and push to ECR") {
                    steps {
                        script {
                            docker.withRegistry(env.ECR_REGISTRY) {
                                def customImage = docker.build("contacts-service")
                                /* Push the image to the ECR */
                                customImage.push()
                            }
                        }
                    }
                }
            }
        }
    }
}
