pipeline {
    agent any
    stages {
        stage('build') {
           steps {
                sh 'mvn -Dmaven.test.failure.ignore=true install' 
            }
        }
         stage('Tests') {
            steps {
                sh 'mvn test'
            }
             post {
                success {
                    junit 'target/surefire-reports/**/*.xml' 
                }
            }
        }
    }
}
