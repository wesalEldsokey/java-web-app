  // 1- Post attribte 
  // 2- Conditions
  // 3- Envirnment variable 
  // 4- Two way to define credentials in jeninsfile (Global => {Env var} ,,, Per stage => {with credentials})
  // 5- Access build Tools for your projects
  // 6- parameters => for some additional configuration that you want to provide in your build to change some behavior 
  //                  ex : If I want to some which version of the application I want to deploy 
  // 7- using groovy script




// IF i want to define my own env var I use enviroment object 
// Another use case of invireoment variable is CREDITIONAL 
// First we define jenkins credentials in jenkins GUI 
// Then using envireoment variable we use ${redentials('credentialId')}  function
  // credentials may be Golbal So we define as an env var in enviroment 
  // or we need this crediential for one stage So we use withcredientials
def gv 
 
pipeline {
  agent any  
  tools {
   // # 3 tools that jenkinsfile support (mvn, gradle and jdk)
   maven 'maven-3.8' 
  }
   parameters {
//   //  String (name: 'VERSION' , defaultValueL '', description: '')
//     choice(name: 'VERSION' ,choices: ['1.1.0' , '1.2.0'] ,description: '')
 booleanParam (name: 'scapeTest' ,defaultValue: true ,description : '')
  }
  environment {
    NEW_VERSION = '1.3.0'
  //  SERVER_CREDENTIALS = credentials('server-creadentials')
  }
  stages {
    
    stage ("init") {
      steps {   
        script {
          gv = load "script.groovy"
        }
        
        
        echo 'building the application'
           }
    }
    
    
    
    
    stage ("build") {
      steps {
        script {
          gv.buildApp()
        }
            }
                    }
    stage ("test"){
     // you may want to run a stage under condiions  SO we use "Conditionals" 

//         expression {
//                     BRANCH_NAME == 'main' || BRANCH_NAME == 'dev'
//                     }
//            }     
 
      when { 
        expression {
          params.scapeTest  
          
        }
      }
        
      steps {
        script{
          gv.testApp()
        } 
            }
                  }
    
    
    
    stage ("depoly"){
      steps {
        script {
         gv.deployApp()
        }
//         echo "deploying the application ${params.VERSION}"
        //echo "depolying with ${SERVER_CREDENTIALS}"
        //sh "${SERVER_CREDENTIALS}"
//         withcredentials([
//               usernamePassword(credentials: 'server-creadentials' , usernameVariable: USER , passwordVariable: PASS)
//         ]) {
         // sh "sone script ${USER} ${PWD}"
//            }
      }
    } }
  post {
    always {
           echo "Hiiiiiii"
           }
       }


}
