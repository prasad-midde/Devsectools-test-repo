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
                           sh "git init"
			   sh "git secrets --install -f "
                           sh "git secrets --register-aws"
                           sh "git secrets --list"
                           sh "git secrets --add 'MyPASSWORD[0-9]+'"
                           sh "git secrets --add 'aws_access_key_id'"
                           sh "git secrets --add 'aws_secret_access_key'"
	                   sh "git secrets --scan -r ."
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
