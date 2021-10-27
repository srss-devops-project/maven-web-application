node
{

     def mavenHome = tool name: "maven 3.8.2"	

     stage('CodeCheckOut') {
     git branch: 'master', credentialsId: 'c5c1b999-d4dc-41f1-b5d1-c44b6accd42b', url: 'https://github.com/srss-devops-project/maven-web-application.git'
	}
     stage('Build'){
     sh "${mavenHome}/bin/mvn clean package"
	}
     stage('ExecutingSonarQubeReport'){
     sh "${mavenHome}/bin/mvn clean sonar:sonar"
	}
	   stage('UploadArtifactsIntoNexusRepository'){
     sh "${mavenHome}/bin/mvn clean sonar:sonar deploy"
	}
     stage('DeployTheAppIntoTomcat'){
     sshagent(['5808d159-dfe3-435a-bd63-9db7ba40e096']) {
     sh "scp -o  StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.128.232:/opt/apache-tomcat-9.0.53/webapps"
	} 
	}
     stage('EmailNotification'){
     mail bcc: 'gsrinivasulu053@gmail.com', body: '''Build Over!!

     Regards 
     SR Software Solutions
     8978502719''', cc: 'gsrinivasulu053@gmail.com', from: '', replyTo: '', subject: 'Build Over!!', to: 'gsrinivasulu053@gmail.com'
	}

}//closingNode
