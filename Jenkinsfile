         pipeline {
             agent any
             
             tools {
                 maven 'mvn'
             }
             
             stages {
                 stage("Git Checkout") {
                     steps {
                         script {
                             git branch: 'main', url: 'https://github.com/Parasharam-Desai/salary-api.git'
                         }
                     }
                 }
                 
                 stage("Bug Analysis ") {
                     steps {
                         script {
                             sh 'mvn compile'
                             sh 'mvn spotbugs:spotbugs'
                             sh 'mvn site'
                         }
                     }
                 }
                 
                 stage('Publish HTML Report') {
                     steps {
                         script {
                             publishHTML([
                                 allowMissing: false,
                                 alwaysLinkToLastBuild: true,
                                 keepAll: true,
                                 reportDir: 'target/site',
                                 reportFiles: 'spotbugs.html',
                                 reportName: 'SpotBugs Report'
                             ])
                         }
                     }
                 }
             }
         }
