node {
  def server = Artifactory.server 'artifactserver.jfrog.io'
  def myMavenContainer = docker.image('maven:3.2-jdk-7')
  myMavenContainer.pull()
  stage('prep') {
    checkout scm
  }
  stage('build') {
     myMavenContainer.inside("-w /usr/src/mymaven") {
       sh 'mvn compile'
     }
  }
  stage('test') {
     myMavenContainer.inside("-w /usr/src/mymaven") {
       sh 'mvn package'
     }
  }
  stage('publish') {
    def uploadSpec = """{
      "files": [
        {
          "pattern": "target/gs-maven-0.1.0.jar",
          "target": "libs-release/chanpreet_new/first-artifact.jar"
        }
     ]
    }"""
    server.upload(uploadSpec)
  }

stage('sonar-scanner') {
      def sonarqubeScannerHome = tool name: 'sonar', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
      withCredentials([string(credentialsId: 'sonar', variable: 'sonarLogin')]) {
        sh "${sonarqubeScannerHome}/bin/sonar-scanner -e -Dsonar.host.url=http://sonarqube:9000 -Dsonar.login=${sonarLogin} -Dsonar.projectName=maven java with sonar -Dsonar.projectVersion=${env.BUILD_NUMBER} -Dsonar.projectKey=GS -Dsonar.sources=complete/src/main/ -Dsonar.tests=complete/src/test/ -Dsonar.language=java"
      }
    }
}


