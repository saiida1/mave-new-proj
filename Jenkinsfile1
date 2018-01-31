
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



stage('publish') {
docker.withRegistry('http://index.docker.io/v1', 'dockerhub')
 def app = docker.build('chanpreet88/test1/', '.').push()

}

  

}
