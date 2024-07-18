pipeline {
    agent any
    
    tools {
        maven 'local_maven'
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

        stage ('Deploy'){
            steps {
                deploy adapters: [tomcat9(credentialsId: '6e9319ef-2452-4385-b4b6-9617c9e5a346', path: '', url: 'http://172.208.115.46:8070/')], contextPath: 'test-java', war: '**/*.war'
            }
        }
    }
}
