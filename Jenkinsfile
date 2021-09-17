  // 1- Post attribte 
  // 2- Conditions
  // 3- Envirnment variable 
  // 4- Two way to define credentials in jeninsfile (Global => {Env var} ,,, Per stage => {with credentials})
  // 5- Access build Tools for your projects
  // 6- parameters => for some additional configuration that you want to provide in your build to change some behavior 
  //                  ex : If I want to some which version of the application I want to deploy 




// IF i want to define my own env var I use enviroment object 
// Another use case of invireoment variable is CREDITIONAL 
// First we define jenkins credentials in jenkins GUI 
// Then using envireoment variable we use ${redentials('credentialId')}  function
  // credentials may be Golbal So we define as an env var in enviroment 
  // or we need this crediential for one stage So we use withcredientials
pipeline {
  agent any  
  tools {
   // # 3 tools that jenkinsfile support (mvn, gradle and jdk)
   maven 'maven-3.8' 
  }
  parameters {
    String (name: 'VERSION' , defaultValueL '', description: '')
 

  }
  environment {
    NEW_VERSION = '1.3.0'
    SERVER_CREDENTIALS = credentials('server-creadentials')
  }
  stages {
    
    stage ("build") {
      steps {
        echo 'building the application'
            }
                    }
    stage ("test"){
      when {
    // you may want to run a stage under condiions  SO we use "Conditionals" 

//         expression {
//                     BRANCH_NAME == 'main' || BRANCH_NAME == 'dev'
//                     }
//            }
      
      steps {
        echo 'testing the application'
        echo "Building version ${NEW_VERSION}"
            }
                  }
    
    
    
    stage ("depoly"){
      steps {
        echo 'deploying the application'
        //echo "depolying with ${SERVER_CREDENTIALS}"
        //sh "${SERVER_CREDENTIALS}"
        withcredentials([
              usernamePassword(credentials: 'server-creadentials' , usernameVariable: USER , passwordVariable: PASS)
        ]) {
          sh "sone script ${USER} ${PWD}"
           }
            }
                    }
  }
  post {
    always {
           echo "Hiiiiiii"
           }
       }


}
