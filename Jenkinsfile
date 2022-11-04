pipeline {
 agent {label 'tomcat-node'}
  triggers {
    pollSCM('* * * * *')
  }
 tools {
    maven 'maven'
  }
  stages{
       stage ('Build'){
        steps {
         sh 'mvn clean package'
        }
         post {
           success {
             echo 'Archiving...'
             archiveArtifacts artifacts:'**/target/*.war'
           }
         }
       }
       stage ('Deployments') {
         parallel{
           stage ('Deploy to Staging'){
             steps {
               sh "cp /home/jenkins/workspace/pipeline_as_code/webapp/target/*.war /opt/tomcat-staging/apache-tomcat-10.0.27/webapps/"
             }
           }
           stage ('Deploy to prod') {
             steps {
               sh "cp /home/jenkins/workspace/pipeline_as_code/webapp/target/*.war /opt/tomcat-prod/apache-tomcat-10.0.27/webapps/"
             }     
           }
         }
       }
    }
} 
  
