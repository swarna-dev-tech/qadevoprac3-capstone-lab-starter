pipeline {
    agent any
    environment {
        TF_VAR_gcp_project = "<your GCP project ID here>" // REPLACE WITH YOUR PROJECT ID FROM QWIKLABS
    }
    stages {
        stage("Configure Cluster") {
            steps {
                script {
                    dir('terraform') {
                        withCredentials([file(credentialsId: 'gcp_credentials', variable:'GCP_CREDENTIALS')]) {
                            sh '''
                            export GOOGLE_APPLICATION_CREDENTIALS=$GCP_CREDENTIALS
                            terraform init
                            terraform apply -auto-approve
                            terrascan scan -i terraform -t gcp
                            '''
                            // TODO: fill in the steps necessary to:
                            // - initialise terraform
                            // - scan the terraform files
                            // - provision the defined resources
                        }
                    }
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}
