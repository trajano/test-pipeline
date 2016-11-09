node {
	// Environment setup
    def mvnHome = tool name:'maven-3.3.9', type:'maven'
    env.PATH = "${mvnHome}/bin:${env.PATH}"
    
    stage("Checkout") {
        checkout scm
    }

	slackSend "Build started - ${env.JOB_NAME} ${env.BUILD_NUMBER} (${env.BRANCH_NAME})"
    try {
	    if (env.BRANCH_NAME == "master") {
	        stage("Build") {
	            mvn 'deploy site'
	        }
	        stage("Code quality analysis") {
	            withSonarQubeEnv {
	                mvn 'org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
	            }
	        }
	        boolean release = false
	        stage("Confirm release") {
	            try {
	                timeout(time: 1, unit: 'MINUTES') {
	                    input 'Release to Central?'
	                    release = true
	                }
	            } catch (ignored) {
	            }
	        }
	        if (release) {
	            stage("Release") {
	                echo "mvn 'release:prepare'"
	                echo "mvn 'release:perform'"
	            }
	        }
	    } else {
	        stage("Build") {
	            mvn 'install site'
	        }
	    }
		slackSend "Build finished - ${env.JOB_NAME} ${env.BUILD_NUMBER} (${env.BRANCH_NAME})"
    } catch (error) {
		slackSend "Build aborted - ${env.JOB_NAME} ${env.BUILD_NUMBER} (${env.BRANCH_NAME}) - ${error}"
	}
}

@NonCPS
def mvn(String args) {
	sh "mvn --batch-mode ${args}"
	junit allowEmptyResults: true, testResults: '**/target/surefire-reports/*.xml'
}
