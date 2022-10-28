pipeline {
    agent any
    environment {
        IBM_ENTITLEMENT_KEY = credentials('ibm_entitlement_key')
        ADMIN_PASSWORD      = credentials('admin_password')
        RELEASE_NAME        = "ibm-test"        
        NAMESPACE           = "dp"
        LICENSE             = "L-RJON-CCAT5F"
        USE                 = "production"
        VERSION             = "10.5.0.2"
    }
    stages {
        stage('Pre Deploy') {
            steps {
                echo 'Pre-Deploy ~ setup configuration before deploy'
                sh('./scripts/01-pre-deploy.sh ${IBM_ENTITLEMENT_KEY} ${RELEASE_NAME} ${NAMESPACE} ${ADMIN_PASSWORD}')
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy ~ deploy DataPowerService'
                sh('./scripts/02-deploy.sh ${RELEASE_NAME} ${NAMESPACE} ${LICENSE} ${USE} ${VERSION}')
            }
        }
        stage('Test Service') {
            steps {
                echo 'Test Service'
                sh('./scripts/03-test-service.sh ${RELEASE_NAME}')
            }
        }
    }
}
