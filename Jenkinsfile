node {
    // Environment setup
    mvnHome = tool name:'maven-3.3.9', type: 'maven'
    env.PATH = "${mvnHome}/bin:${env.PATH}"
    sh 'env'

    stage "Checkout from SCM"
    checkout scm

    stage "Build project"
    if (env.BRANCH_NAME == "master") {
        // deploy SNAPSHOT if master
        sh 'mvn deploy site'
    } else {
        sh 'mvn install site'
    }
    stage "Publish Maven Site"
    junit allowEmptyResults: true, testResults: '**/target/test-reports/*.xml'
    publishHTML([allowMissing: true, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'target/site', reportFiles: '**', reportName: 'Maven Site'])

    stage "Code Quality Analysis"

}
