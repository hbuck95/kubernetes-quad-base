import groovy.json.JsonSlurper

def getAcrLoginServer(def acrSettingsJson) {
  def acrSettings = new JsonSlurper().parseText(acrSettingsJson)
  return acrSettings.loginServer
}


node{
	stage('Azure Login'){
		steps{
			withCredentials([azureServicePrincipal('jenkins')]) {
			// login Azure
			sh '''
			az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID
			az account set -s $AZURE_SUBSCRIPTION_ID
			'''
			// get login server
			def acrSettingsJson = sh script: "az acr show -n $acrName", returnStdout: true
			def loginServer = getAcrLoginServer acrSettingsJson
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



