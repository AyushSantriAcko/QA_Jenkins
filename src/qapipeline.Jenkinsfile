pipeline {
    agent any
    environment {
        QA_JOB_ENDPOINT = "http://staging-build.acko.in/job/Test_Renewal_Revamp/"
        JENKINS_DEV_TOKEN = "MTFiMWY5YzFlOWRmNWZiMGU2MmIyMjg3ZTZjNjViMjgwMg=="
    }
    stages {
        stage ('Run test') {
            agent {
                label 'master'
            }
            build : "Test_Renewal_Revamp"
//             parallel {
//               stage("Test_Renewal_Revamp") {
//               build: Test_Renewal_Revamp
//               }
//             }
            steps{
                sh "curl --silent -X POST ${QA_JOB_ENDPOINT}/buildWithParameters --header 'Authorization: Basic ${JENKINS_DEV_TOKEN }"
            }
        }
    }
}