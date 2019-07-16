pipeline{
	agent any
	stages{	
		stage('pwd'){
			steps{
				sh "pwd"
				sh "ls -alrt"
			}
		}
		stage('clean mongo'){
			steps{
				sh "kubectl delete -f ./mongo/."
			}
		}
		stage('clean server'){
			steps {
				sh "kubectl delete -f ./server/."
			}
		}
		stage('clean client'){
			steps {
				sh "kubectl delete -f ./client/."
			}
		}
		stage('run mongo'){
			steps{
				sh "kubectl apply -f ./mongo/."
			}
		}
		stage('run server'){
			steps{
				sh "kubectl apply -f ./server/."
			}
		}
		stage('run client'){
			steps{
				sh "kubectl apply -f ./client/deployment.yaml"
				sh "kubectl apply -f ./client/service.yaml"

			}
		}
	}
}
