pipeline {
    agent any

    stages {
        stage('拉取代码') {
            steps {
                echo 'Building..'
                //git(changelog: false, credentialsId: 'github-user-pwd', poll: false, url: 'https://github.com/PYxy/argo-cd.git')
                sh '''ls -al'''
                echo "拉取完成"
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
