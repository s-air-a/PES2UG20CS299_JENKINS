pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'g++ -o sample sample.cpp'
                build 'PES2UG20CS299-1'
                echo 'Build stage successful'
            }
        }

        stage('Test') {
            steps {
                sh './sample'
                echo 'Test stage successful'
            }
        }

        stage('Deploy') {
            when{
                expression{
                    currentBuild.result == null || currentBuild.result=='SUCCESS'
                }
            }
            steps {
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
