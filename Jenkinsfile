node('appserver')
{
    def appserver
    stage('Cloning Git')
    {
    /* Let's make sure we have the repository cloned to our workspace */
    checkout scm
    }

    stage('Build-and-tag')
    {
        /* This builds the actual image;
        * This is synonymous to docker build on the command line */
        app = docker.build("samevam/realestate")
    }

    stage('Post-to-dockerhub')
    {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub_credentials')
        app.push("latest")
    }

    stage('Pull-image-server')
    {
        sh "docker-compose down"
        sh "docker-compose up -d"
    }
}