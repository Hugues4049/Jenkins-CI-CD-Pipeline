pipeline {
    agent any

    environment {
        MY_CREDENTIALS = credentials('773c3a8a-126b-494e-a480-098b5ef8c324')
        git_credential = credentials('86ef7c91-1b23-4696-82ad-ae726c0e7aaf')
        }

    stages {
        stage('Create a Staging'){
            steps {
                sh 'git checkout staging'
            }
        }


        stage('Checkout') {
            steps {
            git branch: 'my test branch',
            credentialsId: '86ef7c91-1b23-4696-82ad-ae726c0e7aaf',
            url: 'https://github.com/Hugues4049/Jenkins-CI-CD-Pipeline'
            }
        }

        stage('Build from github') {
            steps {
               
            sh 'docker build -t jenkins . -t hugues4049/ci_docker:latest'
            sh 'docker run -d jenkins'
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
                sh 'docker push hugues4049/ci_docker:latest'
            }
        }
        stage('Merge to Main') {
            steps {
                sh 'git merge origin/main'
                sh 'git push'
            }
        }
    }
}