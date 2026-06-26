pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps { // <--- 여기가 중요합니다. stage 안에 steps가 있어야 합니다.
                checkout scm
            }
        }
        
        stage('Maven Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        
        // 나머지 스테이지들...
    }
}
