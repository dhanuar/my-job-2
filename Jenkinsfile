pipeline{
    agent any
    triggers {
      pollSCM '* * * * *'
    }
    stages{
        stage("maven build"){
            when{
                expression{
                    env.BRANCH_NAME.equals("develop") ||
                    env.BRANCH_NAME.startsWith("feature")
                }
            }
            steps{
              sh "mvn package"
            }
        }
        stage("sonarQube"){
            when{
                expression{
                    env.BRANCH_NAME.equals("develop") ||
                    env.BRANCH_NAME.startsWith("feature")
                }
            }
            steps{
              echo "sonar qube analysis..."
            }
        }
        stage("nexus"){
            when{
                branch "develop3"
            }
            steps{
              nexusArtifactUploader artifacts: [[artifactId: 'myweb', classifier: '', file: 'target/myweb-0.0.5.war', type: 'war']], credentialsId: 'nexus3', groupId: 'in.javahome', nexusUrl: '172.31.42.193:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven--app', version: '0.0.5'
            }
        }
        stage("deploy to qa"){
            when{
                branch "qa"
            }
            steps{
              echo "deplyment to qa"
            }
        }
        stage("deploy to production"){
            when{
                branch "master"
            }
            steps{
              echo "deplyment to master"
            }
        }
    }
}
