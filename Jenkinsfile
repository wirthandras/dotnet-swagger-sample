pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'dotnet build'
            }
        }
        stage('Docker') {
            steps {
              //The following step assuming you have a local nexus3 artifactory with docker registry exposed on port 8082 and
              // NEXUS_CREDENTIAL set for accessing this nexus3 repository from jenkins
              withDockerRegistry([ credentialsId: "NEXUS_CREDENTIAL", url: "http://localhost:8082/" ]) {
                dir('WaSwagger') {
                    sh 'docker build -t localhost:8082/waswagger:1.0 .'
                    sh 'docker push localhost:8082/waswagger:1.0'
                }
              }
            }
        }
    }
}