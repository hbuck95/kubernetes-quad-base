pipeline{
	agent any
	stages{	
		stage('pwd'){
			steps{
				sh "pwd"
				sh "ls -alrt"
			}
		}
		stage('Kill Client'){
			steps{
                        	sh "kubectl delete -f client/."
	                }
		}
		stage('Kill Server'){
			steps{
                        	sh "kubectl delete -f server/."
	                }
		}
		stage('Kill Mongo'){
			steps{
                        	sh "kubectl delete -f mongo/."
	                }
		}
		stage('Run Mongo'){
			steps{
                        	sh "kubectl apply -f mongo/."
	                }
		}
		stage('Run Server'){
			steps{
                        	sh "kubectl apply-f server/."
	                }
		}
		stage('Run Client'){
			steps{
                        	sh "kubectl apply -f client/."
	                }
		}
		stage('Run Nginx'){
			steps{
                        	sh "kubectl apply -f nginx/config-map.yaml"
				sh "kubectl apply -f nginx/deployment.yaml"
	                }
		}
	}
}
