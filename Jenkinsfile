pipeline {
 agent none
 parameters {
   string(name: 'ECRURL', defaultValue: '437030480074.dkr.ecr.ap-south-1.amazonaws.com/', description: 'Please Enter ECR REGISTRY URL with / at the end')
   string(name: 'IMAGE', defaultValue: 'wezvaappimage:3', description: 'Please Enter the Image to Deploy?')
   password(name: 'PASSWD', defaultValue: '', description: 'Please Enter your Gitlab password')
 }
 stages {
  stage('Deploy')
  {
    agent { label 'demo' }
    steps { 
        git branch: 'springboot', credentialsId: 'GitlabCred', url: 'https://gitlab.com/wezvaprojects/ninjas/deployments.git'
	 	dir ("./functionaltest") {
	      sh "sed -i 's/image:.*/image: $ECRURL$IMAGE/g' deployment.yaml" // make sure the ECRURL has \/ at the end
	    }
		sh 'git commit -a -m "New deployment for Build $IMAGE"'
		sh "git push https://scmlearningcentre:$PASSWD@gitlab.com/wezvaprojects/ninjas/deployments.git"
    }
  }
 }
}

