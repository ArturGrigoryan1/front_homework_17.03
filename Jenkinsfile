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
    environment {
        hash=env.hash.substring(0, 7)
    }
    stages {
        stage('check connection') {
            steps {
                echo 'Hello world'
                echo env.base
                echo env.hash
            }
        }
        stage('build front image,push docker hub') {
            steps {
                 withCredentials([string(credentialsId: 'github-token', variable: 'token'), 
                                  string(credentialsId: 'docker-token', variable: 'dockertoken')]
                                ){
                     sh 'docker build -t front-image:$hash .'
                     sh 'docker images'
                     sh 'docker login --username=arturgrigoryan1 --password=$dockertoken'
                     sh 'docker tag front-image:$hash arturgrigoryan1/front:$hash'
                     sh 'docker push arturgrigoryan1/front:$hash'
                     
                     sh '''if [ -d devops_homework_17.03 ];
                     then
                         rm -r devops_homework_17.03
                     fi
                     '''
                     sh 'git clone https://github.com/ArturGrigoryan1/devops_homework_17.03.git'
                     
                     sh '''cd devops_homework_17.03
                     git config --global user.email "arturishkhanich@gmail.com"
                     git config --global user.name "Artur"
                     python3 front.py
                     git add .
                     git commit -m "change in frontend"
                     git remote remove origin
                     git remote add origin https://ArturGrigoryan1:$token@github.com/ArturGrigoryan1/devops_homework_17.03.git
                     git remote -v
                     git push --set-upstream origin main
                     '''         
                 }
            }
        }
    }
}
