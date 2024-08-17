pipeline {
    agent { label 'dotnet8' }
    options {
        timeout(time: 1, unit: 'HOURS') 
    }
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('SCM') {
            steps {
                git url: 'https://github.com/dummyrepos/nopCommerceaug24.git',
                    branch: 'develop'
            }
        }
        stage('Build') {
            steps {
                sh '/usr/bin/dotnet build -c Release src/Presentation/Nop.Web/Nop.Web.csproj'
                sh 'mkdir published && /usr/bin/dotnet publish -o ./published -c Release src/Presentation/Nop.Web/Nop.Web.csproj'
            }
            post {
                success {
                    zip zipFile: './published.zip',
                        archive: true,
                        dir: './published'
                }
            }
        }
    }
}