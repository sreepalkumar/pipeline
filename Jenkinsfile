pipeline {
    agent any

//	tools {
//		jdk 'jdk11'
//	}
//	environment {
//		M2_INSTALL = "/usr/bin/mvn"
//	}

    stages {
        stage('Clone-Repo') {
	    	steps {
	        	checkout scm
	    	}
        }

        stage('Build') {
            steps {
                sh 'mvn install -Dmaven.test.skip=true'
            }
        }
		
        stage('Unit Tests') {
            steps {
                sh 'mvn compiler:testCompile'
                sh 'mvn surefire:test'
                junit 'target/**/*.xml'
            }
        }

        stage('Deployment') {
            steps {
                sh 'sshpass -p "sreepalkumar" scp target/gamutgurus.war sreepalkumar@172.17.0.2:/home/sreepalkumar/Distros/apache-tomcat-9.0.80/webapps'
                sh 'sshpass -p "sreepalkumar" ssh sreepalkumar@172.17.0.2 "/home/sreepalkumar/Distros/apache-tomcat-9.0.80/bin/startup.sh"'
            }
        }
    }
}
