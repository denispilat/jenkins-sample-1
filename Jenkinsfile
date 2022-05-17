// Powered by Infostretch 

timestamps {

node () {

	stage ('APP-IC - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git-login', url: 'https://github.com/denispilat/jenkins-sample-1.git']]]) 
	}
		
	
	stage ('APP-IC - Build') {
	  withMaven(maven: 'Maven') { 
		if(isUnix()) {
			sh "mvn clean package " 
		} else { 
			bat "mvn clean package " 
		} 
	  } 
	}
	
	stage('Deploy') {
	   withMaven(maven: 'Maven') { 
		if(isUnix()) {
			sh "mvn clean deploy" 
		} else { 
			bat "mvn clean deploy" 
		} 
	  } 
	} 

	stage ('APP-IC - Post build actions') {
	// Mailer notification
	step([$class: 'Mailer', notifyEveryUnstableBuild: true, recipients: 'jenkins.orsys@gmail.com', sendToIndividuals: false])
	}
	
}
}
