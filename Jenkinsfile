node {
    mvnHome = tool name:'maven-3.3.9', type: 'maven'
    env.PATH = "${mvnHome}/bin:${env.PATH}"

    stage "Checkout from SCM"
    checkout scm
    // if not release
    stage "Build project"
    // if not master

    stage "Code Quality Analysis"
}
