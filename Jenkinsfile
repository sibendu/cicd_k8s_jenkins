pipeline {

  environment {
    PROJECT = "sibendu"
    DOCKER_REPO = "sibendudas"
    APP_NAME = "hello"
    FE_SVC_NAME = "${APP_NAME}-frontend"
    CLUSTER = "jenkins-cd"
    CLUSTER_ZONE = "us-east1-d"
    IMAGE_TAG = "${DOCKER_REPO}/${PROJECT}_${APP_NAME}:${env.BRANCH_NAME}.${env.BUILD_NUMBER}"
    JENKINS_CRED = "${PROJECT}"
  }
	
  agent none		
/*
  agent {
    kubernetes {
      label 'sample-app'
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
labels:
  component: ci
spec:
  # Use service account that can deploy to all namespaces
  serviceAccountName: cd-jenkins
  containers:
  - name: kubectl
    image: gcr.io/cloud-builders/kubectl
    command:
    - cat
    tty: true
"""
}
  }
*/  
  
  stages {
  	/*
    stage('Test') {
      steps {
        container('kubectl') {
          sh("kubectl get nodes")
        }
      }
    }	
    */
    
    stage('Permissions') {
      steps {
         sh """
            pwd
            echo "GIT_BRANCH=${gitBranch}" >> /etc/environment
            echo "GIT_COMMIT=${gitCommit}" >> /etc/environment
            //gradle test
            println "Stage test completed - ${currentBuild.fullDisplayName}"
         """
      }
    }
    
    stage('Cleanup') {
      steps {
        sh """
            pwd
            echo "GIT_BRANCH=${gitBranch}" >> /etc/environment 
            echo "GIT_COMMIT=${gitCommit}" >> /etc/environment
            //gradle test
            println "Stage test completed - ${currentBuild.fullDisplayName}"
         """
      }
    }
       
  }
   
}
