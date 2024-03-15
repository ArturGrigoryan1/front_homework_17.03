pipeline {
    agent { label 'jenkins_agent' }
    triggers {
    GenericTrigger(
        genericVariables: [
            [defaultValue: '', key: 'base', regexpFilter: '', value: '$.ref'],
            [defaultValue: '', key: 'hash', regexpFilter: '', value: '$.after']
            
            ],
     causeString: 'Triggered on $base',
     token: 'abc123',
     tokenCredentialId: '' )
    }
    stages {
        stage('Check branch name') {
            steps {
                echo 'Hello world'
                echo env.base
                echo env.hash
                
                sh 'ls -la'
            }
        }
        stage('check merge and run docker') {
            steps {
              sh 'docker build -t front-image .'
              sh 'docker images'
              sh 'docker login --username=arturgrigoryan1 --password=dckr_pat_ayRg57qqBcNSEesQv5yv0GW07Rk'
              sh 'docker tag front-image arturgrigoryan1/front-image'
              sh 'docker push arturgrigoryan1/front-image'
            }
        }
    }
}
