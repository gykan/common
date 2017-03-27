#!groovy

node {
    stage('Fetch') {
        checkout scm
    }
    stage('Assemble') {
        sh './gradlew clean build -x test'
    }
    stage('Test') {
        sh './gradlew test'
    }
    stage('Publish') {
        sh './gradlew publish'
    }
}