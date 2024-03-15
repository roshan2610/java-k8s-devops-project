pipeline {
    agent {
        docker {
            image "openjdk:11"
        }
    }

    stages {
        stage("Sonar Quality Check") {
            steps {
                script {
                    try {
                        withSonarQubeEnv(credentialsId: 'sonar-token') {
                            sh 'chmod +x gradlew'
                            sh './gradlew sonarqube'
                        }
                    } catch (Exception e) {
                        echo "SonarQube analysis failed: ${e.message}"
                        currentBuild.result = 'FAILURE'
                    }
                }
            }
        }    
    }
}



// pipeline{
//     agent any
//     stages{
//         stage("Sonar Quality Check"){
//             agent {
//                 docker {
//                     image "openjdk:11"
//                 }
//             }
//             steps{
//                 script{
//                     withSonarQubeEnv(credentialsId: 'sonar-token') {
//                             sh 'chmod +x gradlew'
//                             sh './gradlew sonarqube'
//                     }
//                 }
//             }
//         }    
//     }
// }