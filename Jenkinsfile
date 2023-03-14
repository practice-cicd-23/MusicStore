pipeline {
    agent { label 'DOTNET6'}
    triggers { pollSCM('* * * * *') }
    stages {
        stage('vsc') {
            steps {
                git url: 'https://github.com/practice-cicd-23/MusicStore.git',
                    branch: 'main'
            }
        }
        stage('build') {
            steps {
                sh 'dotnet restore ./MusicStore/MusicStore.csproj && dotnet build ./MusicStore/MusicStore.csproj'
            }
        }
        stage('test') {
            steps {
                sh 'dotnet test --logger "junit;LogFilePath=TEST-musicstoretest.xml" ./MusicStoreTest/MusicStoreTest.csproj'
                junit testResults: '**/TEST-*.xml'
            }
        }
    }
    post {
        success {
            mail subject: "Jenkins Build of ${JOB_NAME} with id ${BUILD_ID} is success",
            body: "Use this URL ${BUILD_URL} for more info",
            to: 'team-all-qt@qt.com',
            from: 'navinreddy3416@gmail.com'
        }
        failure {
            mail subject: "Jenkins Build of ${JOB_NAME} with id ${BUILD_ID} is failed",
            body: "Use this URL ${BUILD_URL} for more info",
            to: "${GIT_AUTHOR_EMAIL}",
            from: 'devops@qt.com'
        }
    }
}