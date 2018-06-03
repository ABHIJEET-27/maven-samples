pipeline {
    agent any
    stages {
        stage('SCM') {
            steps {
                git url: 'https://github.com/ABHIJEET-27/maven-samples.git'
            }
        }
        stage('build && SonarQube analysis') {
            steps {
					withSonarQubeEnv('sonar') {
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
       
		stage('show package & reports on console') {
			steps {
				archiveArtifacts '**/target/**/*.war'
				archiveArtifacts '**/target/**/*.jar'
				junit '**/target/**/surefire-reports/**/*.xml'
				}
			}
		 stage("Quality Gate") {
            steps {
                timeout(time: 0.0833333, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
                }
            }
        }
	  }
	}
