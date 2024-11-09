pipeline {
    agent any

    stages {
        stage('Hello'){
            steps {
                sh '''
                    echo "Hey there Earth"
                    whoami
                    touch container-no.txt
                '''
            }
        }
    }
}