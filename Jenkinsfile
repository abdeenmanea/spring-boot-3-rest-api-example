pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/abdeenmanea/spring-boot-3-rest-api-example.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Stop Old Service') {
            steps {
                sh 'pkill -f spring-boot-3-rest-api-example.jar || true'
            }
        }

        stage('Start Service') {
            steps {
                sh '''
                    JAR_FILE=$(ls target/*.jar | head -n 1)
                    nohup java -jar $JAR_FILE --server.port=8081 > app.log 2>&1 &
                    echo $! > app.pid
                '''
            }
        }
    }
}
