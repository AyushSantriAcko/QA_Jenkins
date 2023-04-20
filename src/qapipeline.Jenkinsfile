pipeline {
    agent any
    environment {
        QA_JOB_ENDPOINT = "http://staging-build.acko.in/job/Test_Renewal_Revamp/"
        JENKINS_DEV_TOKEN = "MTFiMWY5YzFlOWRmNWZiMGU2MmIyMjg3ZTZjNjViMjgwMg=="
        BUILDSTATUS = "FAILURE"
    }
    stages {
        stage ('Run test') {
            parallel {
                agent {
                    label 'master'
                }
                stage("Test_Renewal_Revamp") {
                    steps{
                        echo "Steps"
                        script {
                            def handle = triggerRemoteJob job: "${QA_JOB_ENDPOINT}", auth: CredentialsAuth(credentials: 'JENKINS_QA_API_TOKEN'), shouldNotFailBuild: true
                            BUILDSTATUS = handle.getBuildResult().toString()
                            echo BUILDSTATUS;
                            if (BUILDSTATUS == "FAILURE") {
                               error('Test job failure')
                            }
                        }
                    }
                }
            }

        }
    }
}

// curl --silent -X POST http://staging-build.acko.in/job/Test_Renewal_Revamp/=uat --header 'Authorization: Basic MTFiMWY5YzFlOWRmNWZiMGU2MmIyMjg3ZTZjNjViMjgwMg=='