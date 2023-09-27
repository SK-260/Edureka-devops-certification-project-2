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
                sh ' gradlew build'
            }
    //         post{
    //             always{
    //                 echo "========always========"
    //             }
    //             success{
    //                 echo "========A executed successfully========"
    //             }
    //             failure{
    //                 echo "========A execution failed========"
    //             }
    //         }
    //     }
    // }
    // post{
    //     always{
    //         echo "========always========"
    //     }
    //     success{
    //         echo "========pipeline executed successfully ========"
    //     }
    //     failure{
    //         echo "========pipeline execution failed========"
    //     }
    }
}
}