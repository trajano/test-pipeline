node {
    // Environment setup
    mvnHome = tool name:'maven-3.3.9', type: 'maven'
    env.PATH = "${mvnHome}/bin:${env.PATH}"
    sh 'env'

    stage "Checkout from SCM"
    checkout scm

    // if not release
    stage "Build project"
    if (env.BRANCH_NAME == "master") {
        sh 'mvn deploy site'
    } else {
        sh 'mvn install site'
    }
    // if not master
    stage "Publish Maven Site"
    junit allowEmptyResults: true, testResults: '**/target/test-reports/*.xml'

    stage "Code Quality Analysis"
}
