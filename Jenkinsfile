
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
	//agent any
	agnet {docker { image 'maven:3.6.3'} }
	stages {
      stage('build'){
		  steps{
			  sh 'mvn --version'
			echo "Build"
		 } 

	    }
     stage('Test'){
		  steps{
			echo "Test"
		 } 

	    }
	 stage('Integration Test'){
		  steps{
			  echo "Integration Test"
		 } 

		}
	}

}
