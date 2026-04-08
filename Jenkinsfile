pipeline {
    agent any
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }

    stages {

        stage("build") {
            steps {
                sh 'mvn clean deploy'
            }
        }

        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'vinay-sonar-scanner'
	// tool name is taken from manage Jenkins => systems => tools           
            }

            steps {
                withSonarQubeEnv('vinay-sonarqube-server') { 
	// env name is taken from manage Jenkins => systems => system                                      	  
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
       
    }
}

