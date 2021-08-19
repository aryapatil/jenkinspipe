pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven3.8"
    }

    stages {
		stage ('Test'){
			steps{
					for(int i=0;i<2;i++){
					stage "Stage#" + i
					print 'hello, world!'
			
				if(i==0){
					git "https://github.com/capgteam/bankappgradle.git"
					echo "Running on Stage#0"
				}
				else{
					build "Declarative pipeline"
					echo "Running on Stage#1"
				}
				}
			}
		}
	
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/capgteam/bankapp.git'

                // Run Maven on a Unix agent.
                //sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                 bat "mvn -f Day1-BankApp\\pom.xml -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'Day1-BankApp/target/*.jar'
                }
            }
        }
    }
}