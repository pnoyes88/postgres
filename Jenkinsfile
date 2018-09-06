node('NODE NAME') 
{ 
    withEnv([REQUIRED ENV VARIBALES]) 
    {   withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'CREDENTIALS ID', passwordVariable: 'PW', usernameVariable: 'USER']]) 
        {   try 
                {   stage 'Build' 
                        checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: gitbranch]], doGenerateSubmoduleConfigurations: false, 
                                  extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'CREDENTIALS ID', 
                                  url: 'GIT URL']]]

                                ****
                                MAVEN BUILD
                                ****

                    stage 'Docker Image build & Push'
                                *****
                                DOCKER BUILD AND PUSH TO REPO
                                *****
                }
              catch (err) {
                notify("Failed ${err}")
                currentBuild.result = 'FAILURE'
                }

                stage 'Deploy to ENV'

                *****
                DEPLOYMENT TO REQUIRED ENV
                *****

                notify('Success -Deployed to Environment')

                catch (err) {
                 notify("Failed ${err}")
                currentBuild.result = 'FAILURE'
                } 
        }   
    }
}

def notify(status)
{
****
NOTIFICATION FUCNTION
****
}
