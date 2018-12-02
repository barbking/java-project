properties([pipelineTriggers([githubPush()])])

node('linux') {   
  	stage('Test') {    
		git 'https://github.com/barbking/java-project.git'
		sh 'ant -f test.xml -v'
		junit 'reports/result.xml'  
	}   
	stage('Build') {    
		sh 'ant -f build.xml -v'   
	}   
	stage('Deploy') {    

	}
	stage('Reports') {    
		sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'  
	}
}
