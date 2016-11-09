#!/usr/bin/env groovy
node {
    mvn = tool name:'maven-3.3.9', type: 'maven'
     env.PATH = "${mvn}/bin:${env.PATH}"

    stage "Checkout from SCM"
        sh 'ls -lR'

    // if not release
    stage "Build project"

    stage "Code Quality Analysis"
    withSonarQubeEnv {
        sh 'env'
        sh 'echo ' + mvn
    }
}
