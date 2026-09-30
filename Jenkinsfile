pipeline {
    agent { label 'dotnet' }
    options {
        timeout ( time: 1, unit: 'HOURS' )
    }
    parameters {
        string( name: 'branch', defaultValue : 'main')
        string( name: 'giturl', defaultValue: 'https://github.com/shalu-233/samples.git' )
        string( name: 'BUILDPATH', defaultValue: 'core/hosting/src/DotNetLib/DotNetLib.csproj')
        string( name: 'directory', defaultValue: 'published')
    }
    stages {
        stage ('scm') {
            steps {
                git branch: "${params.branch}",
                    url: "${params.giturl}"
            }
        }
        stage ('build') {
            steps {
                sh "dotnet build -c Release ${params.BUILDPATH}"
                sh "mkdir ${params.directory} && dotnet publish -o ./${params.directory} -c Release ${params.BUILDPATH}"
            }
        }
    }
    post {
        success {
            echo "this is completed"
        }
    }
}