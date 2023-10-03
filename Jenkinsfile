pipeline {
    agent any
    stages {
        stage("build") {
            steps {
                sh "./mvnw package"
            }
        }
        stage("capture") {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar'
                junit '**/target/surefire-reports/TEST*.xml'
                jacoco()
            }
        }
    }
    post {
        always {
            emailext body: "${env.BUILD_URL}\n${currentBuild.absoluteUrl}", 
                to: 'always@foobar',
                recipientProviders: [developers()], 
                subject: "${currentBuild.currentResult}: Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]"
        }
    }
}