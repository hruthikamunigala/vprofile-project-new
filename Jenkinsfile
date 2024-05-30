pipeline {
   agent any
	tools {
        maven "MAVEN3"
        jdk "OracleJDK8"
    }

    environment {
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = '123456'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-maven-central'
        NEXUSIP = '172.31.1.195'
        NEXUSPORT = '8081'
	    NEXUS_GRP_REPO= 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }
	
    stages {
        stage('BUILD'){
            steps {
              sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
              success {
                    echo 'Now Archiving.'
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('TEST'){
            steps {
                sh 'mvn test'
            }
        }
        stage ('CHECKSTYLE ANALYSIS') {
            step {
                sh 'mvn checkstyle:checkstyle'
            }
        }
    }
}
