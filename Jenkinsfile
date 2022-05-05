pipeline {
    agent {
        label 'cicd'
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

            withCredentials([usernamePassword(credentialsId: 'DockerHub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh """
                docker login -u ${USERNAME} -p ${PASSWORD}
                docker push iamsrinathks/sample-nginx:$BUILD_NUMBER
                """
             }
          }
      }
        stage('Deploy to dev') {
            steps {
            sh """
               docker-compose up -d -e TAG=$BUILD_NUMBER
            """

            }
        }
    }
}
