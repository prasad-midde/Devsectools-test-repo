pipeline {	
	agent any
	
	stages {
	      stage('Cloning Git') {
	        steps {
	              checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/prasad-midde/Devsectools-test-repo.git']]])
	        }
	       }
	    stage('git-secrets-check') {
	         steps {
                           sh "git init"
			   sh "git secrets --install -f "
                           sh "git secrets --aws-provider"
			   sh "git secrets --add '(ACCESS|access|Access)'"
	                   sh "git secrets --scan -r ."
	                }
	        }
    
    stage('hadolint-scan') {
	         steps {
	       echo "#######"	 
               echo 'Docker linting/vulnerability scan using hadolint'
               sh 'docker run --rm -i hadolint/hadolint < Dockerfile'
	       echo "#######" 
	      }
	    }
     stage('checkov-scan') {
	         steps {
	       echo "#######"
               echo 'Checking the quality of the code using checkov'
               sh 'checkov -f ./Dockerfile'
               echo "#######"
	       
	      }
	    }
	
	}
	}
