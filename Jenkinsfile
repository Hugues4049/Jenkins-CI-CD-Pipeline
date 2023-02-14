pipeline {
    agent any

    environment {MY_CREDENTIALS = credentials('773c3a8a-126b-494e-a480-098b5ef8c324')}

    stages {
        stage('Staging'){
            steps {
                sh 'git checkout staging'
            }
        }
        stage('Build from github') {
            steps {
               
            sh 'docker build -t jenkins .'
            }
        }
        stage('Test') {
            steps {
                sh 'python -m pip install flask'
                sh 'python -m unittest'
            }
        }
        stage('deploy to dockerhub') {
            steps {
                sh 'docker login -u $MY_CREDENTIALS_USR -p $MY_CREDENTIALS_PSW'
                sh 'docker push hugues4049/ci_docker:tagname'
            }
        }
    }
}