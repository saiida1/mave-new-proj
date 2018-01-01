
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



stage('packages') {

sh 'docker run --rm -w /usr/src/mymaven maven:3.2-jdk-7 mvn package'

}

  

}
