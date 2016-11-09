node {
    mvnHome = tool name:'maven-3.3.9', type: 'maven'
    env.PATH = "${mvnHome}/bin:${env.PATH}"

    stage "Checkout from SCM"
    sh 'ls -lR'

    // if not release
    stage "Build project"
    // if not master
        sh 'mvn install'

    stage "Code Quality Analysis"
    withSonarQubeEnv {
        sh 'env'
        sh 'echo ' + mvn
    }
}
