pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
        git 'git'
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
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: 'Nexus', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.201:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'VinaysDevopsLab-SNAPSHOT', version: '0.0.4-SNAPSHOT'
            }
        }

        // stage4 : Print Environment Variables

        stage ('Print Environment Variables') {
            steps {
                echo "ArtifactId is ${ArtifactId}"
                echo "Version is ${Version}"
                echo "GroupId is ${GroupId}"
                echo "Name is ${Name}"
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