pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                git(url: 'https://github.com/PYxy/argo-cd.git', credentialsId: 'github-user-pwd', branch: '$BRANCH_NAME', changelog: true, poll: false)
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'docker tag nginx:v1  120.132.118.90/harbor-test/nginx-ljy:1.0'
          withCredentials([usernamePassword(credentialsId : 'harbor-user-pwd')]) {
            sh '''echo "Harbor12345" | docker login 120.132.118.90 -u admin --password-stdin
docker push 120.132.118.90/harbor-test/nginx-ljy:1.0'''
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
