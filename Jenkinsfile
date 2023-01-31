pipeline{
    //Directives
    agent any
    tools {
        maven 'Maven'
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
        // stage 3 : publish the artifacts
        stage ('publish to Nexus'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: 'be6dbfc8-abd6-4ba3-800b-df6217b98c6e', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.195:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'vinaysdevops-SNAPSHOT', version: '0.0.4-SNAPSHOT'
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


        // stage 5 : Deploying
        stage ('Deploy'){
            steps {
                echo 'deploying.....'
            }
        }
    }
}
