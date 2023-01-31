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
                   script {

                def NexusRepo = Version.endsWith("SNAPSHOT") ? "vinaysdevops-SNAPSHOT" : "vinaysdevopslab-release"

                nexusArtifactUploader artifacts: 
                [[artifactId: "${ArtifactId}", 
                classifier: '', 
                file: "target/${ArtifactId}-${Version}.war", 
                type: 'war']], 
                credentialsId: 'be6dbfc8-abd6-4ba3-800b-df6217b98c6e', 
                groupId: "${GroupId}", 
                nexusUrl: '172.20.10.195:8081', 
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
                        echo "Name is '${Name}'"
                        echo "GroupID is '${GroupId}'"
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
