properties([pipelineTriggers([githubPush()])])

node('linux') {   
  	stage('Unit Tests') {
		/*init and run unit tests*/
		git 'https://github.com/barbking/java-project.git'
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'  
	}   
	stage('Build') { 
		/*compile Java application using ant*/
		sh 'ant -f build.xml -v'   
	}   
	stage('Deploy') { 
		/*copy build output jar file into an S3 bucket*/
		sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle* s3://gros0120-demo-seis665-03-fall2018'
	}
	stage('Reports') {
		/*generate a report of the CloudFormation stack resources created in your environment*/
		withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'f20c0a9d-0105-4a7f-b3d7-1bbac019c598', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
   		sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins' 
		}	
	}
}
