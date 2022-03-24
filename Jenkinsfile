pipeline {
    agent any

    stages {
        stage('Clone mainrepo first,  later subrepo') {
            steps {  
                sh '''
                git clone 'https://github.com/Gautham-kukutla/mainrepo.git'
                cd mainrepo
                git submodule init
                git submodule update
                cd subrepo 
                pwd
                ls 
                '''

                stash includes: '*', name: 'myfiles'
                sh '''cd ../../
                rm -rf mainrepo '''
            }}
      stage('Clone mainrepo and subrepo using recursive') {
            steps {  
                sh '''
                git clone --recurse-submodules 'https://github.com/Gautham-kukutla/mainrepo.gi'
                cd mainrepo/subrepo
                pwd
                ls
                cd ../../
                rm -rf mainrepo
                '''
            }}
            stage('unstashing') {
                steps { 
                        sh '''mkdir demo
                              cd demo '''
                        unstash 'myfiles'
                        sh '''ls
                              cd ..
                              rm -rf demo'''
                        
    }}
}}
