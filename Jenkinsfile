pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }
         // Stage : Publish the artifacts to Nexus
        stage ('Publish to Nexus'){
            steps {
              nexusArtifactUploader artifacts: [[artifactId: 'jeanbTokamDevOpsLab', classifier: '', file: 'target/jeanbTokamDevOpsLab-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: 'b283ae09-6017-4fc6-84e6-f0861729e0fb', groupId: 'com.jeanbTokamDevOpsLab', nexusUrl: '172.20.10.5:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'JeanbTokamDevOpsLab-SNAPSHOT', version: '0.0.4-SNAPSHOT'
             }
         }
        // Stage3 : Deploying
        stage ('Deploy'){
            steps {
                echo ' deploying......'
                
            }
        }

        
        
    }

}