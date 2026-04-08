pipeline {
    agent any
    environment {
        PATH = "/opt/maven/bin:$PATH"
    }

    stages {

        stage("build") {
            steps {
		echo "---------- build started -----------"
		
                sh 'mvn clean deploy -Dmaven.test.skip=true'

		echo '---------- build completed -----------'
            }
        }

	 stage("test") {
            steps {
                echo "---------- unit test started -----------"

                sh 'mvn surefire-report:report'

                echo '---------- unit test completed -----------'
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

