pipeline {
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    environment {
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

        // Stage3 : Deploy Artifact to Nexus
        stage ('Deploy to Nexus') {
            steps {
                script { 

                def NexusRepo = Version.endsWith("SNAPSHOT") ? ("VinaysDevopsLab-SNAPSHOT") : ("VinaysDevOpsLab-RELEASE")
                nexusArtifactUploader artifacts: [[artifactId: "${ArtifactId}", 
                classifier: '', 
                file: "target/${ArtifactId}-${Version}.war", 
                type: 'war']], 
                credentialsId: 'Nexus', 
                groupId: "${GroupId}", 
                nexusUrl: '172.20.10.201:8081', 
                nexusVersion: 'nexus3', 
                protocol: 'http', 
                repository: "${NexusRepo}", 
                version: "${Version}"
            }
          } 
        }

        // stage4 : Print Environment Variables

        stage ('Print Environment variables'){
                    steps {
                        echo "Artifact ID is '${ArtifactId}'"
                        echo "Version is '${Version}'"
                        echo "GroupID is '${GroupId}'"
                        echo "Name is '${Name}'"
                    }
        }

        // Stage3 : Deploying
        stage ('Deploy'){
            steps {
                echo ' testing......'

            }
        } 
    }

}