def userInput = true
def didTimeout = false
node {
    stage("Clone infrastructure config to workspace") {
    deleteDir()
        sh '''
        curl -X POST -d env=${ENV} -d region=${REGION} host.docker.internal:3000/infra
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
            terraform output -json  | curl -H 'Content-Type: application/json' -d @- docker.for.mac.localhost:3000/status/env
            var=$(terraform output -json | jq -r '.s3_bucket.value')
            aws s3 cp ./terraform.tfstate s3://$var/state/terraform.tfstate  --region ${REGION}
        '''
        }

}