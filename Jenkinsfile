pipeline {
    agent {
        label 'infra'
    }

    stages {
        stage('Prepare') {
            steps{
                sh 'echo "placeholder"'
            }
        }

        stage('Docker build') {
            steps {
                  sh 'docker build . -t iamsrinathks/sample-nginx:$BUILD_NUMBER'
            }
        }


        stage('Docker push') {
            steps {
              sh 'echo "placeholder"'

            }
        }
        stage('Deploy to dev') {
            steps {
            sh 'echo "placeholder"'

            }
        }
    }
}
