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
        stage('build front image,push docker hub') {
            steps {
                sh 'docker build -t front-image .'
                sh 'docker images'
                sh 'docker login --username=arturgrigoryan1 --password=dckr_pat_ayRg57qqBcNSEesQv5yv0GW07Rk'
                sh 'docker tag front-image arturgrigoryan1/front'
                sh 'docker push arturgrigoryan1/front'
                sh 'ls -la'
                sh '''if [ -d devops_homework_17.03 ];
                then
                    rm -r devops_homework_17.03
                fi
                '''
                sh 'git clone https://github.com/ArturGrigoryan1/devops_homework_17.03.git'
                sh 'ls -la'
                sh '''cd devops_homework_17.03
                ls -la
                echo "ban" >> jnjelu
                cat jnjelu
                git status
                git add .
                git status
                '''
                
            }
        }
    }
}
