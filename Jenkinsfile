#!/usr/bin/env groovy

node{
    stage('Git Checkout'){
        git 'https://github.com/suneelbiyyapu/DevOpsClassCodes.git'
    }
    stage('Compile'){
        withMaven(maven:'MyMaven'){
            sh 'mvn compile'
        }
    }
    stage('Test'){
        try{
            withMaven(maven:'MyMaven'){
                sh 'mvn test'
            }
        }finally{
            junit 'target/surefire-reports/*.xml'
        }
    }
    stage('Package'){
        withMaven(maven:'MyMaven'){
            sh 'mvn package'
        }
    }
}
