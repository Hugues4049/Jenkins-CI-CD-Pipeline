pipeline {
    agent any

    stages {

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
        stage('Deploy') {
            steps {
                echo 'deploying...'
                
            }
        }
        
    }
}