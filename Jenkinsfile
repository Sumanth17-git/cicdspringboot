pipeline {
    agent any
	tools {
		maven 'Maven'
	}
	
	environment {
		PROJECT_ID = 'root-furnace-374507'
                CLUSTER_NAME = 'cluster-1'
                LOCATION = 'us-central1-c'
                CREDENTIALS_ID = 'Kubernetes'		
	}
	
    stages {
	    stage('Scm Checkout') {
		    steps {
			    checkout scm
		    }
	    }
	    
	    stage('Build') {
		    steps {
			    sh 'mvn clean package'
		    }
	    }
	    
	    stage('Build Docker Image') {
		    steps {
			    sh 'whoami'
			    script {
				    myimage = docker.build("sumanth17121988/cicd:2")
			    }
		    }
	    }
	    
	    stage("Push Docker Image") {
		    steps {
			    script {
				    echo "Push Docker Image"
				    withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
            				sh "docker login -u sumanth17121988 -p ${dockerhub}"
				    }
				        sh "docker push sumanth17121988/cicd:2"
				    
			    }
		    }
	    }
	     stage("Run Docker Container") {
		    steps {
	
				    echo "Running Docker Container"
            			    sh 'docker run -d -p 8082:8080 sumanth17121988/cicd:2' 
		    }
	    }
	    
	    
	    
	    
  }
}
