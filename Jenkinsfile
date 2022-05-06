pipeline {
    agent {
        label 'cicd'
    }

    options {
      timestamps()
      timeout(time: 30, unit: 'MINUTES')
    }

    stages {
        stage('Prepare') {
            steps{
                sh 'echo "Preparing the environment"'
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
                sh '''
                    docker login -u ${USERNAME} -p ${PASSWORD}
                    docker push iamsrinathks/sample-nginx:$BUILD_NUMBER
                '''
             }
          }
      }
        stage('Deploy to dev') {
            steps {
            sh '''
                export DEPLOY_IMAGE_TAG=$BUILD_NUMBER
                docker-compose up -d
            '''

            }
        }
    }
}
