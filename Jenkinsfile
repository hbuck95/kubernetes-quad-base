pipeline{
	agent any
	stages{	
		stage('Docker ps'){
			steps{
                        	sh "sudo docker ps"
	                }
		}
	
		stage('Get Pods'){
	                steps{
	                        sh "sudo kubectl get pods"
	                }
	        }
	}
}
