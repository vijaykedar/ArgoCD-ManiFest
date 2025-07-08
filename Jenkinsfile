//---------------------------------------------
// Author: Adam WezvaTechnologies
// Call/Whatsapp: +91-9739110917
//---------------------------------------------

pipeline {
 agent none
 parameters {
   string(name: 'ECRURL', defaultValue: '013623161468.dkr.ecr.ap-south-1.amazonaws.com/', description: 'Please Enter ECR REGISTRY URL with / at the end')
   string(name: 'IMAGE', defaultValue: 'spring-dev:dev66', description: 'Please Enter the Image to Deploy?')
   password(name: 'PASSWD', defaultValue: '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', description: 'Please Enter your Gitlab password')
   choice(name:'branch', choices: ['spring-dev', 'sit', 'pre-prod', 'prod'] ,description: 'select where need to deploy')
 }
 stages {
	 
  stage('Deploy')
  {
    agent { label 'demo' }
    steps { 
        git branch: 'springboot', credentialsId: '6414761f-2f87-4d48-b649-9dcb76e50a81', url: 'https://github.com/vijaykedar/ArgoCD-ManiFest.git'
	   dir ("./${params.branch}") {
              sh "sed -i 's#image:.[0-9][0-9].*#image: $ECRURL$IMAGE#g' deploybackend.yml" // make sure the ECRURL has \/ at the end
	    }

		sh 'git commit -a -m "New deployment for Build ${IMAGE}"'
		sh "git push https://vijaykedar:$PASSWD@github.com/vijaykedar/ArgoCD-ManiFest.git"
    }
  }
 }
}

//---------------------------------------------
// Author: Adam WezvaTechnologies
// Call/Whatsapp: +91-9739110917
//---------------------------------------------
