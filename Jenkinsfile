pipeline {
 agent {label 'tomcat-node'}
  triggers {
    pollSCM('* * * * *')
  }
  stages{
       stage ('Build'){
        steps {
         sh 'mvn package'
        }
         post {
           success {
             echo 'Archiving...'
             archiveArtifacts artifacts:'**/target/*.war'
           }
         }
       }
    }
} 
