pipeline{
agent{
kubernetes{
yaml '''
spec: 
  containers: 
  - name: gradle
    image: gradle:6.3-jdk14
'''
}
}
stages {
        
       /* stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace For Project"
                """
            }
        }
*/
        stage('Code Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM', 
                    branches: [[name: 'master']], 
                    userRemoteConfigs: [[url: 'https://github.com/imharsh2005/week6.git']]
                ])
            }
        }
        stage(' Unit Testing') {
            steps {
                echo "${scmVars.GIT_COMMIT}"
                sh """
                echo "Running Unit Tests"
                """
            }
        }

        stage('Code Analysis') {
            steps {
                sh """
                echo "Running Code Analysis"
                """
            }
        }

        stage('Build Deploy Code') {
            when {
                branch 'develop'
            }
            steps {
                sh """
                echo "Building Artifact"
                """

                sh """
                echo "Deploying Code"
                """
            }
        }

    }   
}

/*podTemplate(containers: [containerTemplate(name: 'gradle',
image: 'gradle:6.3-jdk14',
command: 'sleep',
args: '30d'),
])
{
	node(POD_LABEL){
		stage('Runpipelineagainstagradleproject'){
			git 'https://github.com/imharsh2005/week6.git'
			echo env.BRANCH_NAME
            container('gradle'){
			    
                     stage('debug') {
                        try {
                            echo env.GIT_BRANCH
                            echo env.GIT_LOCAL_BRANCH 
                        }
						catch (exc) {
							echo 'some thing failed'
						}
                     }
                     stage('feature') {
                        if (env.GIT_BRANCH == "origin/feature") {
								echo "I am a feature branch"
                         } else {
							echo "not a feature brnach"
						 }                        
                       }
                      stage('master') {
                        if (env.GIT_BRANCH == "origin/master") {
								echo "I am a MASTER branch"
                         } else {
							echo "not a MASTER brnach"
						 }                        
                       }
                
			}
		}
	}
}*/
