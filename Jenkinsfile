pipeline {
 agent {label 'tomcat-node'}
  triggers {
    pollSCM('* * * * *')
  }
  stages{
       stage ('Build'){
        steps {
          sh 'cd /home/jenkins/workspace/pipeline_as_code'
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
               sh "cp **/target/*.war **/tomcat-staging/webapps"
             }
           }
           stage ('Deploy to prod') {
             steps {
               sh "cp **/target/*.war **/tomcat-prod/webapps"
             }     
           }
         }
       }
    }
} 
  
