pipeline{
    agent any
    tools{
        jdk 'JDK 8'
        gradle 'My Gradle'
    } 
    stages{
        stage("Gradle Build"){
            steps{
                git 'https://github.com/SK-260/Edureka-devops-certification-project-2.git'
                withGradle {
                    sh './gradlew build'
                }
            }
        }
    }
}