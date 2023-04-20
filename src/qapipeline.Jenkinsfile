pipeline {
    agent any
    environment {
        QA_JOB_ENDPOINT = "http://staging-build.acko.in/job/Test_Renewal_Revamp/"
        QA_PINCODE_ENDPOINT = "http://staging-build.acko.in/job/Master_Service_Pincode_Test/"
        MASTER_SERVICE_RENEWAL_TEST = "http://staging-build.acko.in/job/Master_Service_Renewal_Test/"
        MASTER_SERVICE_VARIANT_TEST = "http://staging-build.acko.in/job/Master_Service_Variant_Test/"
        JENKINS_DEV_TOKEN = "MTFiMWY5YzFlOWRmNWZiMGU2MmIyMjg3ZTZjNjViMjgwMg=="
        BUILDSTATUS = "FAILURE"
    }
    stages {
        stage ('Run test') {
            parallel {
                stage("MASTER_SERVICE_VARIANT_TEST") {
                    agent {
                        label 'master'
                    }
                    steps{
                        echo "Steps"
                        script {
                            def handle = triggerRemoteJob job: "${MASTER_SERVICE_VARIANT_TEST}", auth: CredentialsAuth(credentials: 'JENKINS_QA_API_TOKEN'), shouldNotFailBuild: true
                            BUILDSTATUS = handle.getBuildResult().toString()
                            echo BUILDSTATUS;
                            if (BUILDSTATUS == "FAILURE") {
                               error('Test job failure')
                            }
                        }
                    }
                }
                stage("Master Service Pincode") {
                    agent {
                        label 'master'
                    }
                    steps{
                        echo "Steps"
                        script {
                            def handle = triggerRemoteJob job: "${QA_PINCODE_ENDPOINT}", auth: CredentialsAuth(credentials: 'JENKINS_QA_API_TOKEN'), shouldNotFailBuild: true
                            BUILDSTATUS = handle.getBuildResult().toString()
                            echo BUILDSTATUS;
                            if (BUILDSTATUS == "FAILURE") {
                               error('Test job failure')
                            }
                        }
                    }
                }
                stage("MASTER_SERVICE_RENEWAL_TEST") {
                    agent {
                        label 'master'
                    }
                    steps{
                        echo "Steps"
                        script {
                            def handle = triggerRemoteJob job: "${MASTER_SERVICE_RENEWAL_TEST}", auth: CredentialsAuth(credentials: 'JENKINS_QA_API_TOKEN'), shouldNotFailBuild: true
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