
node {

def maven.container = docker.image('maven:3.2-jdk-7')

maven.container.pull()

stage('prep') {

checkout scm 

}

stage('compile') { 

maven.container.inside("-w /usr/src/mymaven" ) {

sh 'mvn compile'

}

stage('package') { 

maven.container.inside("-w /usr/src/mymaven" ) {

sh 'mvn package'

}


stage('compiles') {

maven(mavenInstallationName: 'maven') {

sh 'compile' }


stage('packages') {

sh 'docker run -it --rm -w /usr/src/mymaven maven:3.2-jdk-7 mvn package'

}


}
