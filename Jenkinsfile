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
    stage('Review'){
        withMaven(maven:'MyMaven'){
            sh 'mvn pmd:pmd'
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
    stage('Code Coverage'){
        try{
            withMaven(maven:'MyMaven'){
                sh 'cobertura:cobertura -Dcobertura.report.format=xml'
            }
        }finally{
            cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: '/target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
        }
    }
    stage('Package'){
        withMaven(maven:'MyMaven'){
            sh 'mvn package'
        }
    }
}
