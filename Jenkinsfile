node {
    // Environment setup
    mvnHome = tool name:'maven-3.3.9', type: 'maven'
    env.PATH = "${mvnHome}/bin:${env.PATH}"

    stage("Checkout") {
        checkout scm
    }

    if (env.BRANCH_NAME == "master") {
        stage("Build") {
            mvn 'deploy site'
        }
        stage("Code Quality Analysis") {
            withSonarQubeEnv {
                mvn 'org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
            }
        }
        try {
            timeout(time: 1, unit: 'MINUTES') {
                input 'Release to Central?'
            }
            stage("Release") {
                echo "mvn 'release:prepare'"
                echo "mvn 'release:perform'"
            }
        } catch {
        }
    } else {
        stage("Build") {
            mvn 'install site'
        }
    }

}
@NonCPS
def mvn(String args) {
    sh "mvn --batch-mode ${args}"
    junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
}
