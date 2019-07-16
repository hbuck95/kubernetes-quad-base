pipeline{
	agent any
	stages{
		stage('Azure Login'){
			steps{
				withCredentials([azureServicePrincipal('jenkins')]) {
 					sh 'az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID'
				}
			}
		}
	
		stage('Clean'){
			steps{
                        	sh "kubectl delete -f client/."
	                        sh "kubectl delete -f server/."
	                        sh "kubectl delete -f mongo/."
	                }
		}
	
		stage('Deploy Mongo'){
	                steps{
	                        sh "kubectl apply -f mongo/."
	                }
	        }

		stage('Deploy Server'){
	                steps{
	                        sh "kubectl apply -f server/."
	                }
	        }

		stage('Deploy Client'){
	                 steps{
	                         sh "kubectl apply -f client/."
	                }
	        }
	}
}
