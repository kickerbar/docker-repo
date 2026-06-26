pipeline {
    agent any
    
    environment {
        APP_SERVER_IP = "192.168.30.7"
        IMAGE_NAME = "my-web-app:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build & Transfer') {
            steps {
                // 현재 디렉토리에 Dockerfile이 있어야 빌드됩니다.
                sh "docker build -t ${env.IMAGE_NAME} ."
                // 이미지 전송 (SSH 키 설정이 되어 있어야 합니다)
                sh "docker save ${env.IMAGE_NAME} | ssh root@${env.APP_SERVER_IP} 'docker load'"
            }
        }

        stage('Remote Deploy') {
            steps {
                // 대상 서버에서 deploy.sh 실행
                sh "ssh root@${env.APP_SERVER_IP} '/app/deploy.sh'"
            }
        }
    }
}
