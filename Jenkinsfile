pipeline {
    agent any
    environment {
        token = credentials('caeser-pipline')
        tag = v1.0-32-g39aa53c
        message = realeasing v1.0
        name = release-v2.0
        description = halliluya
        

    }
     
    stages {
        stage('Preparing gradlew') {
            steps {
                sh 'chmod +x gradlew'
            }
        }
        stage('test') {
            steps {
                sh './gradlew test'
            }
        }
        stage('build') {
            steps {
                sh './gradlew build'

            }
        }   
        stage('Release') {
            steps {
                 
                sh 'release=$(curl "User-Agent:sunragnawa" -XPOST -H "Authorization:token $token" --data \'{"tag_name": "$tag", "target_commitish": "main", "name": "$name1", "body": "$description", "draft": false, "prerelease": false}\' "https://api.github.com/repos/sunragnawa/caesarcipher/releases")'
            }
        }    
        stage ('deploying') {
            steps {
                sh 'echo deploying ...'
            }
        }
    }
}
