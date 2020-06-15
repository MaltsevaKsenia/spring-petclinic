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
          steps {
            script {
                def scannerHome = tool 'LocalSonarScanner';
                withSonarQubeEnv("LocalSonar") {
                  sh "${scannerHome}/bin/sonar-scanner.bat"
                }
            }
       }
  }
  post {
        always {
            emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
        }
    }
}
}
