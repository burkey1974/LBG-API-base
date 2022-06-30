pipeline {
    agent any
    environment {
        APP_NAME="lbg-api-app-paul"
        TAG="buildnumber"
        //DOCKERHUB_CREDS=credentials("dockerhub_creds")
	REGISTRY="gcr.io/lbg6-130622"
    }
    stages {
        stage('Test') {
            steps {
                sh "npm install"
                sh "npm test"
            }
        }
        stage('Build') {
            steps {
                sh """
                echo "Building image:"
                docker build -t ${REGISTRY}/${APP_NAME}:${BUILD_NUMBER} .
                echo
                """
            }
        }
        stage('Push') {
            steps {
                //sh "docker login -u $DOCKERHUB_CREDS_USR -p $DOCKERHUB_CREDS_PSW"
                sh """
                echo "Push image to registry:"
                docker push ${REGISTRY}/${APP_NAME}:${BUILD_NUMBER}
                echo
                """
            }
        }
        stage('Deploy') {
            steps {
                //
                sh "kubetcl apply -f kubernetes"
            }
        }
    }
}
