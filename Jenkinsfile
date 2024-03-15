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
                var tag = env.hash.charAt(1)
                sh 'echo tag'
                
            }
        }
        stage('check merge and run docker') {
            steps {
              sh 'docker build front-image:$tag .'
              sh 'docker images'
            
            }
        }
    }
}
