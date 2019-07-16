pipeline{
	agent any
	stages{	
		stage('Docker ps'){
			steps{
                        	sh "docker ps"
	                }
		}
	
		stage('Get Pods'){
	                steps{
	                        sh "kubectl get pods"
	                }
	        }
	}
}
