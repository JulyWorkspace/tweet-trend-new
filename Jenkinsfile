pipeline{
    agent{
        label "maven"
    }
    environment{
        PATH = "/opt/apache-maven-3.9.4/bin:$PATH"
    }
    stages{
        stage("Build"){
            steps{
                echo "==========Start Building Project from dev branch==========="
                sh 'mvn clean install'
            }
        }
        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'practicemydevops-sonar-scanner'
            }
            steps{
                withSonarQubeEnv('practicemydevops-sonarqube-server') { // If you have configured more than one global server connection, you can specify its name
                sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}
