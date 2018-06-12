pipeline {
    agent {
      label "jenkins-gradle"
    }
    parameters {
        string(name: 'VERSION', defaultValue: '6.7.0.1', description: 'Which platform version is this?')
        string(name: 'DOWNLOADURL', defaultValue: 'NONE', description: 'Support Portal URL (from hybris wiki)')
        string(name: 'HASH', defaultValue: 'NONE', description: 'expected md5 hash (Available in support portal, Related Info -> Content Info)')
    }
    environment {
        SUSER = credentials('support-portal-user')
        NEXUS = credentials('nexus')
    }
    stages {
      stage("download & publish release") {
          when {
              expression { params.DOWNLOADURL && params.DOWNLOADURL != 'NONE' }
          }
        steps {
          container('gradle') {
            sh """
            gradle downloadCommerce publishMavenPublicationToMavenRepository \
              -PhybrisVersion="${params.VERSION}" \
              -PdownloadUrl="${params.DOWNLOADURL}" \
              -PexpectedHash="${params.HASH}" \
              -PsupportUser="\$SUSER_USR" \
              -PsupportPassword="\$SUSER_PSW" \
              -PnexusURL="http://\$NEXUS_SERVICE_HOST:\$NEXUS_SERVICE_PORT/repository/maven-releases" \
              -PnexusUser="\$NEXUS_USR" \
              -PnexusPassword="\$NEXUS_PSW"
            """
          }
        }
      }
    }
    post {
      always {
          cleanWs()
      }
    }
}