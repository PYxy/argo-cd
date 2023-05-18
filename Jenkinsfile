pipeline {
    agent any
    parameters {
    string(name: 'BRANCH_NAME', defaultValue: 'master', description: '请选择要发布的分支')
    string(name: 'TAG_NAME', defaultValue: 'snapshot', description: '标签名称，必须以 v 开头，例如：v1、v1.0.0')
    }
    environment { //配置全局变量
    REGISTRY = '192.168.113.122:8858'
    DOCKER_CREDENTIAL_ID = 'harbor-user-pass' //harbor 的用户名密码 在jenkins credentials 里面配置的密钥
    GIT_REPO_URL = '192.168.113.121:28080'    //gitlab 的端口密码
    GIT_CREDENTIAL_ID = 'gitlab-user-pass'    //gitlab 的用户名密码 在jenkins credentials 里面配置的密钥
    KUBECONFIG_CREDENTIAL_ID = 'kubeconfig-id' 
    DOCKERHUB_NAMESPACE = 'docker_username' 
    GITHUB_ACCOUNT = 'root'
    APP_NAME = 'k8s-cicd-demo'
  }
    stages {
        
        stage('拉取代码分支') {
            when {
                branch 'master'  // 只有主分 才做
            }
            steps {
                echo "打印参数(分支):REGISTRY  $REGISTRY"
                echo 'Building..'
                git changelog: false, credentialsId: 'github-user-pwd', poll: false, url: 'https://github.com/PYxy/argo-cd.git'
                sh '''ls -al'''
                sh '''pwd'''
                sh '''docker ps'''
                sh '''kubectl get ns'''
                echo "拉取完成"
            }
        }
        stage('Test') {
            when {
            expression {
             params.BRANCH_NAME == 'master'
             }

            }
            steps {
                input(message: 'deploy to production?', submitter: '') //用于终止 或者继续往下走
//                  sh 'docker tag nginx:v1  120.132.118.90/harbor-test/nginx-ljy:1.0'
//           withCredentials([usernamePassword(credentialsId : 'harbor-user-pwd' ,passwordVariable : 'DOCKER_PASSWORD' ,usernameVariable : 'DOCKER_USERNAME' ,)]) {
//             sh '''echo "$DOCKER_PASSWORD" | docker login 120.132.118.90 -u "$DOCKER_USERNAME" --password-stdin
// docker push 120.132.118.90/harbor-test/nginx-ljy:1.0'''
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
