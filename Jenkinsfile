pipeline {
  agent any
  stages {
      stage('Initialize') {
          steps {
            
                deleteDir() 
            
                checkout scm
           
                script {
                    sh '''
                    echo "PATH = ${PATH}"
                    '''
                } // step echo script
                
                zip archive: true, dir: '.', glob: '', zipFile: 'zomefile.zip'
                step([$class: 'UCDeployPublisher',
                  siteName: 'UCD',
                      
                             
                  component: [
                          $class: 'com.urbancode.jenkins.plugins.ucdeploy.VersionHelper$VersionBlock',
                          componentName: 'Jenkins',
                          createComponent: [
                              $class: 'com.urbancode.jenkins.plugins.ucdeploy.ComponentHelper$CreateComponentBlock',
                              componentTemplate: '',
                              componentApplication: 'Jenkins-APP'
                          ],
                          delivery: [
                              $class: 'com.urbancode.jenkins.plugins.ucdeploy.DeliveryHelper$Push',
                              pushVersion: '${BUILD_NUMBER}',
                              baseDir: '/var/jenkins_home/workspace/tMultibranchPipeline_master-DBIPVKXZ7QNG5SHFYNIO7N4UIDI7SDDUPBFJTAUCIMBJIT3NNLEA/',
                              fileIncludePatterns: '*',
                              fileExcludePatterns: '.*',
                              pushProperties: 'jenkins.server=Local\njenkins.reviewed=false',
                              pushDescription: 'Pushed from Jenkins',
                              pushIncremental: false
                          ],
                  ],
                  deploy: [
                      $class: 'com.urbancode.jenkins.plugins.ucdeploy.DeployHelper$DeployBlock',
                      deployApp: 'JenkinsApplication',
                      deployEnv: 'TestJenkinsEnvironment',
                      deployProc: 'TestJenkinsEnvironmentProcess',
                      createProcess: [
                          $class: 'com.urbancode.jenkins.plugins.ucdeploy.ProcessHelper$CreateProcessBlock',
                          processComponent: 'TestJenkinsEnvironmentProcess'
                      ],
                      deployVersions: 'Jenkins:${BUILD_NUMBER}',
                      deployOnlyChanged: false
                  ]
              ])  //  step UCD
          }  //  steps
      }  //  stage('Initialize')
  } // stages.
} // pipeline
