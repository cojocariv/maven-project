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
    }
} 
