pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    environment{
       ArtifactId = readMavenPom().getArtifactId()
       Version = readMavenPom().getVersion()
       Name = readMavenPom().getName()
       GroupId = readMavenPom().getGroupId()
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
        // Stage3 : Publish the artifacts to Nexus
        stage ('Publish to Nexus'){
            steps {
                script {

                def NexusRepo = Version.endsWith("SNAPSHOT") ? "Tokam-SNAPSHOT" : "Tokam-RELEASE"

                nexusArtifactUploader artifacts: 
                [[artifactId: "${ArtifactId}", 
                classifier: '', 
                file: "target/${ArtifactId}-${Version}.war", 
                type: 'war']], 
                credentialsId: 'b283ae09-6017-4fc6-84e6-f0861729e0fb', 
                groupId: "${GroupId}", 
                nexusUrl: '170.20.10.5:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: "${NexusRepo}", 
                version: "${Version}"
             }
            }
        }
       // Stage 4 : Print some information
        stage ('Print Environment variables'){
                    steps {
                        echo "Artifact ID is '${ArtifactId}'"
                        echo "Version is '${Version}'"
                        echo "GroupID is '${GroupId}'"
                        echo "Name is '${Name}'"
                    }
                }

         // Stage 5 : Deploying        
        stage ('Deploy'){
            steps{
                echo 'deploying.....'
            }
       }
    }
}



    

nexusArtifactUploader artifacts: [[artifactId: 'Tokam', classifier: '', file: 'target/Tokam-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: 'b283ae09-6017-4fc6-84e6-f0861729e0fb', groupId: 'com.tokam', nexusUrl: '172.20.10.5', nexusVersion: 'nexus3', protocol: 'http', repository: 'Tokam-SNAPSHOT', version: '0.0.4'
