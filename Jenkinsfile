pipeline {
            tools
	{
		maven 'MAVEN_HOME'
		jdk 'JAVA_HOME'
                        msbuild 'MSBuild'
	}
agent any
stages {
stage ('Checkout') {
            steps {
                 git credentialsId: 'userId', url: 'https://github.com/manyatripathi/SampleCliApp',branch: 'master'
            }
}
stage ('Restore PACKAGES') {     
         steps {
             sh "dotnet restore --configfile NuGet.Config"
          }
        }
stage('Clean') {
      steps {
            sh 'dotnet clean'
       }
    }
stage('Build') {
     steps {
            sh 'dotnet build --configuration Release'
      }
   }
stage('Pack') {
     steps {
           sh 'dotnet pack --no-build --output nupkgs'
      }
   }
stage('Publish') {
      steps {
           sh "dotnet nuget push **\\nupkgs\\*.nupkg -k yourApiKey -s http://myserver/artifactory/api/nuget/nuget-internal-stable/com/sample"
       }
   }
 }
}
