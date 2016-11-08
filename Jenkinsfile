node {
    mvnHome = tool name:'maven-3.3.9', type: 'maven'

    stage "Checkout from SCM"
    checkout scm

    // if not release
    stage "Build project"
	sh "${mvnHome}/bin/mvn deploy"

    stage "Build site"
	sh "${mvnHome}/bin/mvn site"

    stage "Code Quality Analysis"
    withSonarQubeEnv {
        sh "${mvnHome}/bin/mvn sonar:sonar"
    }
    
    stage "Publish Maven Site"
    // publishHTML (target: [ reportDir: "target/site", reportFiles: 'index.html', reportName: 'Maven Site', keepAll:true ])
}
