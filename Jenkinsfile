node {
    // Environment setup
    mvnHome = tool name:'maven-3.3.9', type: 'maven'
    env.PATH = "${mvnHome}/bin:${env.PATH}"
    sh 'env | sort'

    stage("Checkout from SCM") {
        checkout scm
    }

    if (env.BRANCH_NAME == "master") {
        stage("Build and deploy snapshot") {
            mvn 'deploy site'
        }
        stage("Code Quality Analysis") {
            junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
            withSonarQubeEnv {
                sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
            }
        }
        input message: "Release?"
        stage("Perform maven release") {

        }
    } else {
        stage("Build pull request") {
            mvn 'install site'
            junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
        }
    }

}
@NonCPS
def mvn(String args) {
    sh "mvn ${args}"
    junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
}
