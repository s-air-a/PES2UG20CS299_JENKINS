pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
                sh 'g++ -o sample sample.cpp'
                sh 'curl -X POST http://<jenkins-url>/job/299/build'
                echo 'Build stage successful'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
                sh './sample'
                echo 'Test stage successful'
                post
                  {
                    always
                    {
                      junit 'target/surefire-reports/*.xml'
                    }
                  }
            }
        }

        stage('Deploy') {
            steps {
                sh 'mvn deploy'
                echo 'Deployment successful'
            }
        }
    }

    post {
        failure {
            echo 'Pipeline failed'
        }
    }
}
