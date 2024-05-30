pipeline {
  agent { label 'JENKINS_AGENT' }
  environment {
    CLOUDSDK_CORE_PROJECT='primal-gear-411416'
    CLIENT_EMAIL='jenkins-user@primal-gear-411416.iam.gserviceaccount.com'
    GCLOUD_CREDS=credentials('gcloud-cred')
  }
  stages {
    stage('test') {
      steps {
        sh '''
          gcloud version
          gcloud auth activate-service-account --key-file="$GCLOUD_CREDS"
          gcloud compute zones list
        '''
      }
    }
	
	stage('get cluster info') {
		steps {
			sh '''
			  gcloud container clusters get-credentials jenkins-cicd-gke-cluster-1 --zone us-east1-d --project primal-gear-411416
			  kubectl cluster-info
			  kubectl get nodes -o wide
			'''  
		}
	}
  }
}