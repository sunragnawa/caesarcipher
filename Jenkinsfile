pipeline {
    agent any
    environment {
        token = credentials('caeser-pipline')
        tag = "$(git describe --tags)"
        message = "$(git for-each-ref refs/tags/$tag --format=\'%(contents)\')"
        name = "$(echo $message | head -n1)"
        description = "$(echo $message | tail -n +3)"
        

        

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
                 
                sh 'release=$(curl "User-Agent:sunragnawa" -XPOST -H "Authorization:token $token" --data \'{"tag_name": "$tag", "target_commitish": "main", "name": "$name", "body": "$description", "draft": false, "prerelease": false}\' "https://api.github.com/repos/sunragnawa/caesarcipher/releases")'
            }
        }    
        stage ('deploying') {
            steps {
                sh 'echo deploying'
            }
        }
    }
}
