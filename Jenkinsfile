pipeline{
	agent any
	environment {
		TAG = "${git rev-parse HEAD}"
	}
	stages{	
		stage('Get Hash'){
			steps{				
				sh '$TAG'
			}
		}
		stage('Set Version'){
                        steps{
				sh 'sed -i \"s/{{TAG}}/\${TAG}/g\" ./client/deployment.yaml'
				sh 'sed -i \"s/{{TAG}}/\${TAG}/g\" ./server/deployment.yaml'
			}
                }
                stage('Build Client'){
                        steps{
				sh 'sudo docker build ./client/. -t hbuck/client:$TAG'
                        }
                }
                stage('Build Server'){
                        steps{
				sh 'sudo docker build ./client/. -t "hbuck/server:$TAG'				
                        }
                }
                stage('Push'){
                        steps{
                                sh '''sudo docker push hbuck/client:$tag
				'''
				sh '''sudo docker push hbuck/server:$tag
				'''
                        }
                }
		stage('Clean Nginx'){
			steps{
				sh "kubectl delete -f ./nginx/config-map.yaml"
				sh "kubectl delete -f ./nginx/deployment.yaml"
			}
		}
		stage('Clean Mongo'){
			steps{
				sh "kubectl delete -f ./mongo/."
			}
		}
		stage('Clean Server'){
			steps {
				sh "kubectl delete -f ./server/."
			}
		}
		stage('Clean Client'){
			steps {
				sh "kubectl delete -f ./client/deployment.yaml"
				sh "kubectl delete -f ./client/service.yaml"
			}
		}
		stage('Run Mongo'){
			steps{
				sh "kubectl apply -f ./mongo/."
			}
		}
		stage('Run Server'){
			steps{
				sh "kubectl apply -f ./server/."
			}
		}
		stage('Run Client'){
			steps{
				sh "kubectl apply -f ./client/deployment.yaml"
				sh "kubectl apply -f ./client/service.yaml"
			}
		}
		stage('Run Nginx'){
			steps{
				sh "kubectl apply -f ./nginx/."
			}
		}
	}
}
