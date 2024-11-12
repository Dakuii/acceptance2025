pipeline {
    agent any
    stages {
    
    stage("Package"){
    	steps{
    	sh "./gradlew build"
    	}
    }
    
    stage("Docker build"){
    	steps{
    	sh "docker build -t localhost:5000/calculatrice ."
    	}
    }
       
     
     
     
}
}

