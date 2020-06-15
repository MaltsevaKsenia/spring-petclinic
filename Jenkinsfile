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
       stage("SonarQube Analysis") {
          agent any
          steps {
            script {
                def scannerHome = tool 'LocalSonarScanner';
                withSonarQubeEnv("LocalSonar") {
                  sh "${scannerHome}/bin/sonar-scanner"
                }
            }
       }
  }
}
}
