pipeline {
    agent any


//	environment {
//		M2_INSTALL = "/home/gamut/Distros/apache-maven-3.6.0/bin/mvn"
//	}

    stages {
		stage('Clone-Repo') {
			steps {
				checkout scm
			}
		}
		stage('Build') {
	    	steps {
				sh 'mvn install -DskipTests'
			}
	    }
		stage('Unit Tests') {
			steps {
				sh 'mvn surefire:test'
			}
		}
		stage('Deployment') {
	    	steps {
				sh 'sshpass -p "swarna99" scp target/gamutkart.war swarna@172.17.0.3:/home/softwaers/apache-tomcat-8.5.43/webapps'                                   
				sh 'sshpass -p "swarna99" ssh swarna@172.17.0.2 "JAVA_HOME=/home/softwaers/jdk1.8.0_221" "/home/softwaers/apache-tomcat-8.5.43/bin/startup.sh"'
	        	}
		}
    }
}
