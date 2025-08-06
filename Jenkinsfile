pipeline {
    agent any
    tools {
        maven "MAVEN17"
        jdk "JDK17"
    }
    
    environment {
        SNAP_REPO = 'vpro-snap'
		NEXUS_USER = 'admin'
		NEXUS_PASS = 'admin@123'
		RELEASE_REPO = 'vprofile-release'
		CENTRAL_REPO = 'vpro-maven-central'
		NEXUSIP = '172.31.91.92'
		NEXUSPORT = '8081'
		NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }
            post {
                success {
                    echo 'Archiving artifacts...'
                    archiveArtifacts artifacts: '**/*.war'
                }
                
            }
        }
        stage ('test') {
            steps {
                script {
                    sh 'mvn -s settings.xml test'
                    }
            }
        }
        stage ('Checkstyle Analysis') {
            steps {
                script {
                    sh 'mvn -s settings.xml checkstyle:checkstyle'
                }
            }
        }
    }
}