pipeline {
    agent { label 'master' }
    stages {
    stage ('Checkout code')
    {
    context="continuous-integration/jenkins/"
    context += isPRMergeBuild()?"pr-merge/checkout":"branch/checkout"
    checkout scm
    setBuildStatus ("${context}", 'Checking out completed', 'SUCCESS'
                    }

    stage ('Build')
                    {
    mvn 'clean install -DskipTests=true -Dmaven.javadoc.skip=true -Dcheckstyle.skip=true -B -V'
                    }
    stage ('Unit tests')
                    {
    mvn 'test -B -Dmaven.javadoc.skip=true -Dcheckstyle.skip=true'
    if (currentBuild.result == "UNSTABLE") {
        sh "exit 1"
    }
                    }
}   
