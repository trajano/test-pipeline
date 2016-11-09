node {
    stage "Checkout from SCM"
    checkout scm

    stage "Environment Setup"
    mvnHome = tool name:'maven-3.3.9', type: 'maven'
    env.PATH = "${mvnHome}/bin:${env.PATH}"

    // if not release
    stage "Build project"
    // if not master

    stage "Code Quality Analysis"
}
