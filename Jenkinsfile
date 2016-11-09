node {
    // Environment setup
    mvnHome = tool name:'maven-3.3.9', type: 'maven'
    env.PATH = "${mvnHome}/bin:${env.PATH}"
    sh 'env | sort'

    stage "Checkout from SCM"
    checkout scm

    stage "Build project"
    if (env.BRANCH_NAME == "master") {
        // deploy SNAPSHOT if master
        sh 'mvn deploy site'
        stage "Code Quality Analysis"
        withSonarQubeEnv {
            sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
        }
    } else {
        sh 'mvn install site'
        junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
    }
    stage "Publish Maven Site"
    //publishHTML([allowMissing: true, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'target/site', reportFiles: 'index.html', reportName: 'Maven Site'])

}
