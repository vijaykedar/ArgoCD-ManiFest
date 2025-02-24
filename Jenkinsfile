//---------------------------------------------
// Author: Adam WezvaTechnologies
// Call/Whatsapp: +91-9739110917
//---------------------------------------------

pipeline {
 agent none
 parameters {
   string(name: 'ECRURL', defaultValue: '717279694003.dkr.ecr.ap-south-1.amazonaws.com', description: 'Please Enter ECR REGISTRY URL with / at the end')
   string(name: 'IMAGE', defaultValue: 'wezvatechbackend:rel38', description: 'Please Enter the Image to Deploy?')
   password(name: 'PASSWD', defaultValue: '', description: 'Please Enter your Gitlab password')
   choice(name:'branch', choices: ['functional', 'integration', 'regression', 'uat', 'release' ] ,description: 'select where need to deploy')
 }
 stages {
  stage('Deploy')
  {
    agent { label 'demo' }
    steps { 
        git branch: 'springboot', credentialsId: 'GitlabCred', url: 'https://gitlab.com/wezvaprojects/ninjas/deployments.git'
	    dir ("./${params.branch}") {
              sh "sed -i 's/image:.[0-9][0-9].*/image: $ECRURL$IMAGE/g' deploybackend.yml" // make sure the ECRURL has \/ at the end
	    }

		sh 'git commit -a -m "New deployment for Build $IMAGE"'
		sh "git push https://scmlearningcentre:$PASSWD@gitlab.com/wezvaprojects/ninjas/deployments.git"
    }
  }
 }
}

//---------------------------------------------
// Author: Adam WezvaTechnologies
// Call/Whatsapp: +91-9739110917
//---------------------------------------------