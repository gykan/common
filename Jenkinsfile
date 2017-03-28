#!groovy

node {
    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'artifactory-credentials',
                          usernameVariable: 'ARTUSERNAME', passwordVariable: 'ARTPASSWORD'],
                     [$class: 'UsernamePasswordMultiBinding', credentialsId: 'aws-credentials',
                          usernameVariable: 'AWS_ID', passwordVariable: 'AWS_KEY']]) {
        stage('Fetch') {
            checkout scm
        }
        stage('Assemble') {
            sh './gradlew -PartUsername=$ARTUSERNAME -PartPassword=$ARTPASSWORD clean build -x test'
        }
        stage('Test') {
            sh './gradlew -PartUsername=$ARTUSERNAME -PartPassword=$ARTPASSWORD test'
        }
        stage('Publish') {
            sh './gradlew -PartUsername=$ARTUSERNAME -PartPassword=$ARTPASSWORD publish --stacktrace'
        }
    }
}