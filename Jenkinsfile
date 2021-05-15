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

        // Stage3 : Publish artifact to Nexus repo
        stage ('Publish Artificat to Nexus Repo') {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'RakeshDemo', classifier: '', file: 'target/RakeshDemo-0.0.4-SNAPSHOT.war', type: 'war']], credentialsId: '01204525-6731-4ff0-8086-b79ec90275e9', groupId: 'com.rakeshdevopslab', nexusUrl: '172.20.10.152:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'RakeshDevopsLab-SNAPSHOT', version: '0.0.4-SNAPSHOT'
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
