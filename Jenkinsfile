pipeline {
     agent any
     stages {
          stage("Compile") {
               steps {
                    sh "./gradlew compileJava"
               }
          }
         
		   //stage("Code coverage") {
  //   steps {
         // sh "./gradlew jacocoTestReport"
         // sh "./gradlew jacocoTestCoverageVerification"
     //}z
//}
		  
stage("Package") {
     steps {
          sh "./gradlew build"
     }
}

stage("Docker build") {
     steps {
          sh "docker build -t sandyverden/spring-boot-sample ."
     }
}

stage("Docker push") {
     steps {
          sh "docker push sandyverden/spring-boot-sample"
     }
}
stage("Deploy to staging") {
     steps {
		 sh "docker-compose up -d"
     }
}

stage("Acceptance test") {
    steps {
          sleep 60
          //sh "./acceptance_test_docker.sh"
     }
}
     }
	 post {
     always {
         sh "docker-compose down"
     }
}
}
