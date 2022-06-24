pipeline {
    agent any
    environemnt {
        image_name="burkey1974/lbg-API-base:latest"
    stages {
        stage('Test') {
            steps {
                    sh "npm install"
                sh "npm test"
            }
        }
        stage('Build') {
            steps {
                //
                sh """
                echo "building image"
		docker build -t $image_name .
                echo
		"""
            }
        }
        stage('Deploy') {
            steps {
                //
                sh "echo Deploy stage"
            }
        }
    }
}
