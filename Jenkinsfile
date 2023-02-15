pipeline {
    agent any

    environment {
        MY_CREDENTIALS = credentials('773c3a8a-126b-494e-a480-098b5ef8c324')
        }
    stages {
        stage('Checkout'){
            steps {
                sshagent(credentials: ['github_priv_key']){
                    //sh 'git branch --delete staging'
                    sh 'git branch staging'
                    sh 'git checkout staging'
                }
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
                ssshagent(credentials: ['github_priv_key']){
                    sh 'git checkout main'
                    sh 'git pull origin main'
                    sh 'git merge staging'
                    sh 'git push origin main'
                }
            }
        }
    }
}