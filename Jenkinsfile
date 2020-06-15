pipeline {
    agent any
    stages {
        stage('Build') {
           steps {
                sh 'mvn -Dmaven.test.skip=true install' 
            }
        }
         stage('Tests') {
            steps {
                sh 'mvn test'
            }
             post {
                always {
                    junit 'target/surefire-reports/*.xml' 
                }
            }
        }
        stage('Sonarqube') {
            tools {
                sonarQube 'LocalSonarScanner'
           }
          steps {
            withSonarQubeEnv('SonarQube Scanner') {
              sh 'sonar-scanner'
            }
        }
    }
  }
}
