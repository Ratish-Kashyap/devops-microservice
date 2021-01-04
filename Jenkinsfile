
//scripted
//node {
//	stage('Build') {
//		echo "Build"
//	}
//	stage('Test') {
//		echo "Test"
//	}
//}

pipeline {
	 agent any
	//agent {docker { image 'maven:3.6.3'} }
	environment {
     dockerHome = tool 'mydocker'
	 mavenHome = tool 'myMaven'
	 PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
    }	
	stages {
      stage('Checkout'){
		  steps{
			sh 'mvn --version'
			sh 'docker --version' 
			echo "Build"
			echo "PATH - $PATH"
			echo "BUILD_NUMBER - $env.BUILD_NUMBER"
			echo "BUILD_ID - $env.BUILD_ID"
			echo "JOB_NAME - $env.JOB_NAME"
			echo "BUILD_TAG - $env.BUILD_TAG"
			echo "BUILD_URL - $env.BUILDURL"
		 } 

	    }
     stage('Compile'){
		  steps{
			sh "mvn clean compile"
		 } 

	    }
	 stage('Test'){
		  steps{
			  sh "mvn test"
		 } 

		}
	stage('Integration Test'){
		  steps{
			  sh "mvn failsafe:integration-test failsafe:verify"
		 } 

	}
	stage('Package'){
		  steps{
			  sh "mvn package -DskipTests"
		 } 

	}
	stage('Build Docker Image'){
		  steps{
			  //"docker build -t ratishkashyap/jenkins-devops:$env.BUILD_TAG"
			  script{ 
				  dockerImage = docker.build("docker build -t ratishkashyap/jenkins-devops:${env.BUILD_TAG}")
			  } 

		 } 
	stage('Docker Push Image'){
		  steps{
			  //"docker build -t ratishkashyap/jenkins-devops:$env.BUILD_TAG"
			  script{ 
				  docker.withRegistry('', 'dockerhub'){ 
				  dockerImage.push();
				  dockerImage.push('latest');
				   } 
			  } 

		 } 

		}
	}

}
