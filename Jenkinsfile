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
                sh 'dotnet test --logger "junit;LogFilePath=TEST-musicstoretest.xml" ./MusicStoreTest/MusicStoreTest.csproj',
                junit testResults: '**/TEST-*.xml'
            }
        }
    }
}

