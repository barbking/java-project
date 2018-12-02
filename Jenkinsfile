properties([pipelineTriggers([githubPush()])])

node('linux') {   
  	stage('Unit Tests') {    
		git 'https://github.com/barbking/java-project.git'
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'  
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}   
	stage('Deploy') {    
		sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle* s3://gros0120-demo-seis665-03-fall2018'
	}
	stage('Reports') {    
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'awsaccessid', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]){
   		sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins' 
		}	
	}
}
