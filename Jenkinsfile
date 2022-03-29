pipeline {	
	agent any
	stages {
	      stage('Cloning Git') {
	        steps {
	              checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/prasad-midde/test.git']]])
	        }
	       }
	    stage('git-secrets-check') {
	         steps {
                        echo 'Scan'   
	                }
	        }
    
    stage('hadolint-scan') {
	         steps {
               echo 'Docker linting/vulnerability scan using hadolint'
               sh 'docker run --rm -i hadolint/hadolint < ./Dockerfile'         
	      }
	    }
    
	
	}
	}
