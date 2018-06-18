# Hybris Version Download and Publish

This little gradle build leverages the hybris gradle plugin to download the platform
zip from the SAP Support Portal and publishes it to a Maven nexus.

The `Jenkinsfile` is tailored to a default Jenkins-X installation, but requires
two additional secrets (`nexus` for the Nexus admin credentials and
`support-portal-user` for the SAP Support Portal) to be available in Jenkins.