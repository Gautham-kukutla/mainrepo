pipeline {
    agent any

    stages {
        stage('Clone mainrepo first,  later subrepo') {
            steps {  
                sh '''rm -rf mainrepo
                git clone 'https://github.com/Gautham-kukutla/mainrepo.git'
                cd mainrepo
                git submodule init
                git submodule update
                cd subrepo 
                pwd
                ls 
                '''
                dir( './mainrepo/subrepo/' ) {
                stash includes: '*', name: 'myfiles'
                }
            }}
      stage('Clone mainrepo and subrepo using recursive') {
            steps {  
                sh '''
                rm -rf mainrepo
                git clone --recurse-submodules 'https://github.com/Gautham-kukutla/mainrepo.git'
                cd mainrepo/subrepo
                pwd
                ls
                cd ../../
                rm -rf mainrepo
                '''
            }}
            stage('unstashing') {
                steps { 
                        sh '''
                        rm -rf demo
                        mkdir demo
                               '''
                        dir( './demo/' ) {
                        unstash 'myfiles'
                        }
                        sh '''                        
                        ls demo/'''
                        
    }}
}}
