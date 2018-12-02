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
}
