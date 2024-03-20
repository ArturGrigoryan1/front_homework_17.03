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
        registry = "arturgrigoryan1/front"
        registryCredential = 'dockerhub_id'
        dockerImage = ''
    }
    stages {
        stage('check connection') {
            steps {
                echo 'Hello world'
                echo env.base
                echo env.hash
            }
        }
        stage('Building our image') {
                steps{
                    script {
                        dockerImage = docker.build registry + ":$hash"
                    }
                }
        }
        
        stage('Deploy our image') {
            steps{
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push()
                    }
                }
            }
        }
       
        stage('push new image in devops docker-compose') {            
            steps {
                 withCredentials([string(credentialsId: 'github-token', variable: 'token')]
                                ){                    
                     sh '''if [ -d devops_homework_17.03 ];
                     then
                         rm -r devops_homework_17.03
                     fi
                     '''
                     git branch: 'main', url: 'https://github.com/ArturGrigoryan1/devops_homework_17.03.git'
                     sh '''git config --global user.email "arturishkhanich@gmail.com"
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
