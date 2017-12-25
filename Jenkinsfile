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
          "pattern": "complete/target/gs-maven-0.1.0.jar",
          "target": "libs-release/chanpreet/first-artifact.jar"
        }
     ]
    }"""
    server.upload(uploadSpec)
  }
}
