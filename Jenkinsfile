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
                sh '''tag=$(echo env.hash | rev | cut -c34- | rev)
                echo $tag
                sh docker build -t front-image:${tag} .
                '''
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
                git config --global user.email "arturishkhanich@gmail.com"
                git config --global user.name "Artur"
                echo "ban" >> jnjelu
                cat jnjelu
                git status
                git add .
                git status
                git commit -m "change in frontend"
                git remote -v
                git remote remove origin
                git remote -v
                git remote add origin https://ArturGrigoryan1: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@github.com/ArturGrigoryan1/devops_homework_17.03.git
                git remote -v
                git push --set-upstream origin main
                '''
                
    
            }
        }
    }
}
