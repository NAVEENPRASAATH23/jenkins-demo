// pipeline {
//     agent any

//     stages {

//         stage('Build Docker Image') {
//             steps {
//                 bat 'docker build -t naveenprasaath2904/web-app:jen1 .'
//             }
//         }

//         stage('Push Docker Image') {
//             steps {
//                 withCredentials([usernamePassword(
//                     credentialsId: 'dockerhub-creds',
//                     usernameVariable: 'DOCKER_USER',
//                     passwordVariable: 'DOCKER_PASS'
//                 )]) {

//                     bat '''
//                     docker login -u %DOCKER_USER% -p %DOCKER_PASS%
//                     docker push naveenprasaath2904/web-app:jen1
//                     docker logout
//                     '''
//                 }
//             }
//         }
//     }

//     post {
//         success {
//             echo 'Docker image built and pushed successfully!'
//         }

//         failure {
//             echo 'Pipeline failed.'
//         }
//     }
// }



pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t naveenprasaath2904/web-app:jen1 .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {

                    bat '''
                    docker login -u %DOCKER_USER% -p %DOCKER_PASS%
                    docker push naveenprasaath2904/web-app:jen1
                    docker logout
                    '''
                }
            }
        }

        stage('Cleanup') {
            steps {
                bat '''
                docker image rm -f naveenprasaath2904/web-app:jen1
                '''
            }
        }
    }

    post {
        success {
            echo 'Docker image built, pushed and cleaned up successfully!'
        }

        failure {
            echo 'Pipeline failed.'
        }

        always {
            cleanWs()
        }
    }
}
