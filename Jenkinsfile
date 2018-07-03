def userInput = true
def didTimeout = false
node {
    stage("Clone infrastructure config to workspace") {
    deleteDir()
        sh '''
        curl -H 'Content-Type: application/json' --data '{"env":${ENV},"region":${REGION}}' host.docker.internal.localhost:3000/infra
        git clone https://github.com/premutos2003/ct-infra-base.git'''
    }

    stage("Build infrastructure") {
        sh '''
        terraform init ./ct-infra-base
        terraform apply --auto-approve -var aws_access_key=${AWS_ACCESS_KEY} -var aws_secret_key=${AWS_SECRET_KEY} -var region=${REGION}  -var env=${ENV} ./ct-infra-base
    '''
    }
    stage("Get Metadata") {
            sh '''
            bash ct-infra-base/metadata.sh
        '''
        }

}