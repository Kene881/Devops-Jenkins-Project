pipeline {
    agent any

    stages {
        stage('Get source') {
            steps {
                git branch: 'main', url: 'https://github.com/Kene881/Devops-Jenkins-Project.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_TAG}")
                }
            }
        }
        
        stage('Deploy') {
            steps {
                withCredentials(
                    [usernamePassword(
                        credentialsId: 'docker-1', 
                        usernameVariable: 'DOCKER_USER', 
                        passwordVariable: 'DOCKER_PASS'
                    )]
                ) {
                    powershell '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    docker push ${IMAGE_TAG}
                    docker logout
                    '''
                }
                // docker.withRegistry('', '6094d59e-4ff3-4ed4-9a28-64bdf8208789') {
                //     dockerImage.push()
                // }
                // bat """
                // docker push $IMAGE_TAG
                // """
            }
        }
    }
}
