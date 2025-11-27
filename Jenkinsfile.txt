pipeline{

agent any

tools{
maven 'mymaven'
}

parameters{
 choice(name: "ENV",choices: ["","Dev","Test"])
}

stages{
   stage('Build on Dev Env')
   {
     when{   // keyword for if  
      expression{params.ENV == "Dev"}  // condition to be satisfied 
     }
     steps{
      echo "Dev Environment"
     git 'https://github.com/Sonal0409/DevOpsCodeDemo.git'
     sh 'mvn compile'
     }
   }
   stage('Build on Test Env')
   {
   when{   // keyword for if  
    expression{params.ENV == "Test"}  // condition to be satisfied 
   }
   steps{
   git 'https://github.com/Sonal0409/DevOpsCodeDemo.git'
   sh 'mvn test'
   }
   
   }

}
}
