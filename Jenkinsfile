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
                branch "develop"
            }
            steps{
              echo "sonar qube analysis..."
            }
        }
        stage("nexus"){
            when{
                branch "develop"
            }
            steps{
              echo "nexus upload artifacts..."
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
