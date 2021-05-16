pipeline{
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

        // Stage3 : Publish artifact to Nexus repo
        stage ('Publish artifact to Nexus Repo') {
            steps {
                nexusArtifactUploader artifacts:
                [[artifactId: "${ArtifactId}",
                classifier: '',
                file: 'target/RakeshDemo-0.0.4-SNAPSHOT.war',
                type: 'war']],
                credentialsId: '01204525-6731-4ff0-8086-b79ec90275e9',
                groupId: "${GroupId}",
                nexusUrl: '172.20.10.152:8081',
                nexusVersion: 'nexus3',
                protocol: 'http',
                repository: 'RakeshDevopsLab-SNAPSHOT',
                version: "${Version}"
            }
        }

        // Stage4 : Print some information
        stage ('Print Environment Variables'){
            steps {
              echo "ArtifactId is '${ArtifactId}'"
              echo "Version is '${Version}'"
              echo "GroupId is '${GroupId}'"
              echo "Name is '${Name}'"
            }
        }

        // Stage4 : Deploying
        stage ('Deploy'){
            steps {
              echo "Deploying..."
            }
        }
    }
}
