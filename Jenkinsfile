pipeline {
    agent any
    tools {
        maven 'Maven3'
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/priyankabhatnagarcloud-creator/spring-petclinic.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                pkill -f spring-petclinic || true
                JENKINS_NODE_COOKIE=dontKillMe nohup java -jar target/*.jar --server.port=9090 > app.log 2>&1 &
                '''
            }
        }
    }
}