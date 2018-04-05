def userInput = true
def didTimeout = false
node {


    stage("Clone infrastructure config to workspace") {
    deleteDir()
        sh 'git clone https://github.com/premutos2003/ct-infra-base.git'
    }
    stage("Get Metadata") {
                sh '''
                ls
                chmod 400 metadata.sh
                ./ metadata.sh
            '''
            }
    stage("Build infrastructure") {
        sh '''
        terraform init ./ct-infra-base
        terraform apply --auto-approve -var aws_access_key=${AWS_ACCESS_KEY} -var aws_secret_key=${AWS_SECRET_KEY} -var region=${REGION} ./ct-infra-base
    '''
    }
    stage("Get Metadata") {
            sh '''
            bash metadata.sh
        '''
        }

}