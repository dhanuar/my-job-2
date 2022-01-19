pipeline{
    agent any
    triggers {
      pollSCM '* * * * *'
    }
    stages{
        stage("maven build"){
            when{
                branch "develop"
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
