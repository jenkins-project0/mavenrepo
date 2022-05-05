pipeline{
agent {label 'prod server'}

triggers {
        pollSCM '* * * * *'
    }

stages{

stage('scm'){
steps{
checkout([$class: 'GitSCM', branches: [[name: '*/feat01']], extensions: [], userRemoteConfigs: [[credentialsId: 'ea38090f-489e-489e-9008-79a18ad0c620', url: 'https://github.com/jenkins-project0/mavenrepo.git']]])
}
}

stage('build'){
steps{
sh 'mvn package'
}
}

stage('sonar'){
steps{
withSonarQubeEnv('sonarqube') {
    sh 'mvn sonar:sonar'
}

}
}

stage('nexus'){
steps{
sh 'mvn deploy'
}
}

stage('tomcat'){
steps{
sh 'scp /root/workspace/dev/target/studentapp-2.1.1-FEAT01-SNAPSHOT.war /var/lib/tomcat/webapps'
}
}

}
}
