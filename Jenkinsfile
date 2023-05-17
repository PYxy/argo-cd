pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                git(url: 'https://github.com/PYxy/argo-cd.git', credentialsId: 'github-user-pwd')
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
        }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
