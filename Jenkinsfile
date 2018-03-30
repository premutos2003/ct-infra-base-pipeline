def userInput = true
def didTimeout = false
node {


    stage("Clone infrastructure config to workspace") {
    deleteDir()
        sh 'git clone https://github.com/premutos2003/ct-infra-base.git'
    }
    stage("Build infrastructure") {
        sh '''
        cd ct-infra-base
        terraform init
        terraform plan
    '''
    }

}