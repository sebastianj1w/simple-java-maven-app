pipeline {
    agent {
        docker {
            image 'sebastianj1w/maven_with_git:latest'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Fetch') {
	    steps {
		sh 'git fetch origin'
	    }
	}
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
            }
        }
    }
}
