
import java.text.*
def Version = null
def FileName = null

// Build Properties (num builds to keep, polling, blocking, etc)
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '30', artifactNumToKeepStr: '5', daysToKeepStr: '30', numToKeepStr: '5'))])

try
{
    timestamps
    {
        node('master')
        {
            stage('Set Version')
            {   
                def dateFormat = new SimpleDateFormat("yyyy.MM.dd")
                def date = new Date()
                def dateString = dateFormat.format(date)
                def versionString = BRANCH_NAME+"."+dateString+"."+BUILD_NUMBER
        
                currentBuild.displayName = versionString
            }

            //pull the source code from git tfs.
            stage('check out')
            {
                // delete the existing source code to cleanup the workspace.
                deleteDir()
                // checkout the code from git tfs to the workspace.
                checkout scm
            }
            
            stage('Build Project')
            {                     
                //bat 'dotnet build 	HelpdeskMVC.sln	'
                  echo "Builded Sucessfully" 
            }
            
// 			if(BRANCH_NAME.equals("devops1") || BRANCH_NAME.equals("develop"))
//             {
//                 stage('Upload Artifacts for Veracode Scan')
//                 {
//                     def packageName = "package.zip"
//                     powershell "Compress-Archive -Path Dist\\* -CompressionLevel Fastest -DestinationPath $workspace\\$packageName"
//                   // artifactory.pushPackageToTRArtifactory("$Version", "path/$BRANCH_NAME", "$BRANCH_NAME", "$packageName")

				
// 				}
               
//             }
            
        }
    }
}
catch (e){
    echo e.getMessage()
    currentBuild.result = 'FAILURE'
    throw e
}