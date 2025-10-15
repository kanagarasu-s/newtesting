pipeline {
    agent any
    stages {
        stage('Debug Git') {
            steps {
                sh '''
                git ls-remote https://github.com/kanagarasu-s/newtesting.git
                git rev-parse HEAD
                '''
            }
        }
    }
}

