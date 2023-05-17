pipeline {
    agent any

    stages {
        stage('拉取代码') {
            steps {
                echo 'Building..'
                //git(changelog: false, credentialsId: 'github-user-pwd', poll: false, url: 'https://github.com/PYxy/argo-cd.git')
                sh '''ls -al'''
                sh '''docker ps'''
                sh '''kubectl get ns'''
                echo "拉取完成"
            }
        }
        stage('Test') {
            steps {
                 sh 'docker tag nginx:v1  120.132.118.90/harbor-test/nginx-ljy:1.0'
          withCredentials([usernamePassword(credentialsId : 'harbor-user-pwd' ,passwordVariable : 'DOCKER_PASSWORD' ,usernameVariable : 'DOCKER_USERNAME' ,)]) {
            sh '''echo "$DOCKER_PASSWORD" | docker login 120.132.118.90 -u "$DOCKER_USERNAME" --password-stdin
docker push 120.132.118.90/harbor-test/nginx-ljy:1.0'''
                echo 'Testing..'
          }
        }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
