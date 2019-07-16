pipeline{
        agent any
        stages{
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



