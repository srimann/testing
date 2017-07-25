node ("master") {
    stage ("Checkout") {
      checkout([$class: 'GitSCM', 
      branches: [[name: '*/master']], 
      extensions: [[$class: 'CleanBeforeCheckout']], 
      userRemoteConfigs: [[credentialsId: 'GithubCredentials', 
      url: 'https://github.com/quinnliu/sampleGradleProject.git']]])
    }   
    stage ("Build") {
      sh "/opt/gradle/latest/bin/gradle assemble"
      sh "pwd"
      echo "${env.WORKSPACE}"
    }
    stage ("Unit Test")    {
      sh "/opt/gradle/latest/bin/gradle test"
      publishHTML([ 
      reportDir: '/var/lib/jenkins/workspace/gradleproject/build/reports/tests/test', 
      reportFiles: 'index.html', 
      reportName: 'gradleproject TestReport', 
      reportTitles: ''])

    }
    
}   
