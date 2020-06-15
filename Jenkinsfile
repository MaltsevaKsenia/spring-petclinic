pipeline {
    agent any
    environment {
      VERSION = VersionNumber([
        versionNumberString : '${BUILD_YEAR}.${BUILDS_THIS_YEAR}',
        projectStartDate : '2014-05-19'
      ]);
    }
    stages {
        stage('Build') {
           steps {
                sh 'mvn -Dmaven.test.skip=true install -Dproject.version=${VERSION}' 
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
 }
  post {
        always {
             emailext body: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS:Check console output at $BUILD_URL to view the results.', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: '$PROJECT_NAME - Build # $BUILD_NUMBER - $BUILD_STATUS!'
        }
    }
}
