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
        sh 'mvn deploy'
    } else {
        sh 'mvn package'
    }
    // if not master


    stage "Code Quality Analysis"
}
