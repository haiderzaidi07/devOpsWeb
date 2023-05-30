pipeline {
    agent any
    
    tools {
        maven 'localMaven'
    }
    environment {
        fname = "Ranjit"
        lname = "Swain"
        version = "1.2"
        system = "Dev"
    }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
	stage ('Provision EC2 instance'){
		steps {
			sh '''
				cd tf
				terraform init
				terraform destroy -auto-approve
			'''
		}
	}
	stage ('Deploy to Staging'){
	    steps {
		echo "This is made by ${env.fname} ${env.lname}"
		echo "it's running on ${env.system} and the version is ${env.version}"
		//deploy adapters: [tomcat7(credentialsId: 'StagingTomcatServer', path: '', url: 'http://3.110.179.112:8080/')], contextPath: null, war: '**/*.war'
	    }
	}
    }
}
