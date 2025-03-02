pipeline{
    agent any
    tools{
        jdk 'JDK 8'
        gradle 'My Gradle'
    } 
    stages{
        stage('Delete Workspace'){
            steps{
                deleteDir()
            }
        }
        stage("Gradle Build"){
            steps{
                git 'https://github.com/SK-260/Edureka-devops-certification-project-2.git'
                withGradle {
                    sh './gradlew build'
                }
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Test Server', transfers: [
                    sshTransfer(
                        cleanRemote: false, 
                        excludes: '', 
                        execCommand: '', 
                        execTimeout: 120000, 
                        flatten: false, 
                        makeEmptyDirs: false, 
                        noDefaultExcludes: false, 
                        patternSeparator: '[, ]+', 
                        remoteDirectory: '/gradle-project', 
                        remoteDirectorySDF: false, 
                        removePrefix: '', 
                        sourceFiles: 'bin/**, data/**, dist/**, gradle/wrapper/**, test/**, gradlew, gradlew.bat, package.json, package-lock.json, public/**, routes/**, views/**,Dockerfile')], 
                        usePromotionTimestamp: false, 
                        useWorkspaceInPromotion: false, 
                        verbose: false)])
            }
        }
        stage('Build image and push'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Test Server', transfers: [
                    sshTransfer(
                        cleanRemote: false, 
                        excludes: '', 
                        execCommand: '''
                            cd gradle-project
                            docker rmi edureka-project
                            docker login
                            docker build -t sk260/edureka-project2:v1 .
                            docker push sk260/edureka-project2:v1
                        ''', 
                        execTimeout: 120000, 
                        flatten: false, 
                        makeEmptyDirs: false, 
                        noDefaultExcludes: false, 
                        patternSeparator: '[, ]+',
                        remoteDirectory: '', 
                        remoteDirectorySDF: false, 
                        removePrefix: '', 
                        sourceFiles: '')], 
                        usePromotionTimestamp: false, 
                        useWorkspaceInPromotion: false, 
                        verbose: false)])
            }        
        }
        stage('Kubernetes Deployment'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'Kubemaster', transfers: [
                    sshTransfer(
                        cleanRemote: false, 
                        excludes: '', 
                        execCommand: '''
                            cd project-deployment
                            kubectl delete -f deployment.yaml
                            kubectl apply -f deployment.yaml
                        ''', 
                        execTimeout: 120000, 
                        flatten: false, 
                        makeEmptyDirs: false, 
                        noDefaultExcludes: false, 
                        patternSeparator: '[, ]+', 
                        remoteDirectory: 'project-deployment', 
                        remoteDirectorySDF: false, 
                        removePrefix: '', 
                        sourceFiles: 'deployment.yaml')], 
                        usePromotionTimestamp: false, 
                        useWorkspaceInPromotion: false, 
                        verbose: false)])
            }
        }
    }
}