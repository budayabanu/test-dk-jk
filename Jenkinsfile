pipeline {
    agent none
    stages {
        stage ("Docker image build and push") {
            agent any
            stages {
                stage("Docker build and push to ECR") {
                    steps {
                        script {
                            docker.withRegistry(env.ECR_REGISTRY, "ecr:eu-west-1:jenkins-standard-profile") {
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
