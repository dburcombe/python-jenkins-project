pipeline {
    agent any

    stages {
        stage('Presteps') {
           parallel {
               stage('MainBranchPreSteps') {
                   when {
                       anyof {
                           branch "master"
              		   changeRequest targetBranch: 'master', approved: true	 
                       }
                   }
		   steps {
		       echo 'This is the master branch'
		       echo 'installing requirements.txt'
	        	  {
			   sh """
                           python3.8 -m pip install virtualenv
			   python3.8 -m pip install -r requirements.txt
                           deactivate
			   """
                         }
                   }
               }
               stage('NonMainBranchPreSteps') {
                   when {
                       not {
			   anyof {
         	                branch "master"
              		        changeRequest targetBranch: 'master', approved: true	 
 			   }
		       }	
		   }
		   steps {
 		       echo 'This is not the main branch so won't trigger a build.'	    			       }
	       }  	
	       	
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
