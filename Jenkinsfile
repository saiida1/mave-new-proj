node {

def maven.container == docker.image('maven')

maven.container.pull()

stage('prep') {

checkout scm 

}

stage('compile') { 

maven.container.inside("-v ) {

sh 'mvn compile'

}

stage('package') { 

maven.container.inside("-v ) {

sh 'mvn package'

}


stage('compiles') {

maven(mavenInstallationName: 'maven') {

sh 'compile' }


stage('packages') {

sh 'docker run -it --rm -w /usr/src/mymaven maven:3.2-jdk-7 mvn package'

}


}
