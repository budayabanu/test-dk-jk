pipeline {
    agent none
    stages {
        stage ("Docker image build and push") {
            agent any
            stages {
                stage('AWS Login') {
                      steps {
                        script {
                           sh("aws ecr get-login --region=eu-west-1")
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
