node('remote') {
    stage 'Checkout Git project'
    git url: 'https://github.com/MaltsevaKsenia/spring-petclinic'
    def appVersion = version()
    if (appVersion) {
        echo "Building version ${appVersion}"
    }

    stage 'Build Maven project'
    def mvnHome = tool 'M3'
    sh "${mvnHome}/bin/mvn -B -Dmaven.test.failure.ignore verify"
    step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
}
def version() {
    def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
    matcher ? matcher[0][1] : null
}
 
