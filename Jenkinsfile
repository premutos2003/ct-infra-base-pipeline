def userInput = true
def didTimeout = false
node {


    stage("Clone infrastructure config to workspace") {
        sh 'git clone https://github.com/premutos2003/ct-infra-base.git'
    }
    stage("Build infrastructure") {
        sh '''
        cd ct-infra-base
        terraform init
        terraform
        terraform apply --auto-approve -var aws_access_key=${AWS_ACCESS_KEY} -var aws_secret_key=${AWS_SECRET_KEY} -var region=${REGION}

    '''
    }

}