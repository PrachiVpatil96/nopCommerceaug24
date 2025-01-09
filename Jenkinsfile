// pipeline {
//     agent { label 'dotnet8' }
//     options {
//         timeout(time: 1, unit: 'HOURS') 
//     }
//     triggers {
//         pollSCM('* * * * *')
//     }
//     tools {
//         dotnetsdk 'DOTNET8'
//     }
//     stages {
//         stage('SCM') {
//             steps {
//                 git url: 'https://github.com/dummyrepos/nopCommerceaug24.git',
//                     branch: 'develop'
//             }
//         }
//         stage('Build') {
//             steps {
//                 sh 'dotnet build -c Release src/Presentation/Nop.Web/Nop.Web.csproj'
//                 sh 'mkdir published && dotnet publish -o ./published -c Release src/Presentation/Nop.Web/Nop.Web.csproj'
//             }
//             post {
//                 success {
//                     zip zipFile: './published.zip',
//                         archive: true,
//                         dir: './published'
//                 }
//             }
//         }
//     }
// }

pipeline{
    agent { label 'dotnet'}
    options { 
        timeout(time: 1, unit: 'HOURS') 
    }
    stages {
        stage ('PollSCM') {
            steps{
            git url: 'https://github.com/PrachiVpatil96/nopCommerceaug24.git',
                branch: 'main'
            }
        }
        stage ('Restore'){
            steps {
                sh 'dotnet restore src/Presentation/Nop.Web/Nop.Web.csproj'
            }
        }
        stage ('Build') {
            steps {
                sh 'dotnet build --configuration Release src/Presentation/Nop.Web/Nop.Web.csproj'
            }
        }
        stage ('package') {
            steps {
                sh 'mkdir published'
                sh 'dotnet publish --configuration Release --output published/src/Presentation/Nop.Web/Nop.Web.csproj'
            }
        }
    } 


}