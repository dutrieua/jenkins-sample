// Powered by Infostretch 

timestamps {

node () {

	stage ('App-IC - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'github-login', url: 'https://github.com/dutrieua/jenkins-sample.git']]]) 
	}
	stage ('App-IC - Compile') {
 			// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn clean compile " 
			} else { 
 				bat "mvn clean compile " 
			} 
 		} 
	}
	stage ('App-IC - Test') {
 			// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn test" 
			} else { 
 				bat "mvn test" 
			} 
 		} 
	}
	stage ('App-IC - Package') {
 			// Maven build step
	withMaven(maven: 'maven') { 
 			if(isUnix()) {
 				sh "mvn package -DskipTests" 
			} else { 
 				bat "mvn package -DskipTests" 
			} 
 		} 
	}
	stage('Quality check') {
		withSonarQubeEnv('Sonar') {
			bat "mvn sonar:sonar"
		}
	}
	stage ('App-IC - Post build actions') {
/*
Please note this is a direct conversion of post-build actions. 
It may not necessarily work/behave in the same way as post-build actions work.
A logic review is suggested.
*/
		// Mailer notification
		step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'axel.dutrieux@st.com', sendToIndividuals: false])
 
	}
}
}
