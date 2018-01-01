
node {
def myTestContainer = docker.image('maven:3.2-jdk-7')

myTestContainer.pull()
 
stage('prep') {

checkout scm 

}

stage('compile') { 

myTestContainer.inside("-w /usr/src/mymaven" ) {

sh 'mvn compile'

}
}

stage('package') { 

myTestContainer.inside("-w /usr/src/mymaven" ) {

sh 'mvn package'

}
}


stage('compiles') {

maven(mavenInstallationName: 'maven') {

sh 'compile' }

}
stage('packages') {

sh 'docker run -it --rm -w /usr/src/mymaven maven:3.2-jdk-7 mvn package'

}

  stage('docker build/push') {            
     docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
def app = docker.build("chanpreet88/jenkinsfile-demo", '.').push()
     }
  }

}
