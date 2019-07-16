pipeline{
	agent any
	stages{	
		stage('Get Hash'){
			steps{
				sh '''tag=$(git rev-parse HEAD)
				'''
				
				sh '''echo $tag
				'''
			}
		}
		stage('Set Version'){
                        steps{
                               	sh '''sed -i \"s/{{TAG}}/\${tag}/g\" ./client/deployment.yaml
				'''
				sh '''sed -i \"s/{{TAG}}/\${tag}/g\" ./server/deployment.yaml
				'''
			}
                }
                stage('Build Client'){
                        steps{
				sh '''sudo docker build ./client/. -t "hbuck/client:${tag}"
				'''
                        }
                }
                stage('Build Server'){
                        steps{
				sh '''sudo docker build ./client/. -t "hbuck/server:${tag}"
				'''
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
