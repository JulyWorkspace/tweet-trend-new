pipeline{
    agent{
        label "maven"
    }
    environment {
        PATH = "/opt/apache-maven-3.9.4/bin:$PATH"
    }
    stages{
        stage("Build"){
            steps{
                echo "==========Start Building Project from main branch==========="
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "=====================Build Completed========================"
            }
        }

        stage("Test"){
            steps{
                echo "==========Unit Testing Started==========="
                sh 'mvn surefire-report:report'
                echo "==========Unit Test Completed============"
            }
        }

        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'sonar-scanner'
            }
            steps{
                withSonarQubeEnv('sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
                sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}
