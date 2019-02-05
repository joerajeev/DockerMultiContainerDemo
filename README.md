# DockerMultiContainerDemo
This is a demo application that sets up multiple containers to achive a trivial function of calculating the fibonacci numbers for a given index and store the result.
It sets up 6 containers:
 - nginx (for routing)
 - client (the app)
 - server (apis)
 - worker (does the processing)
 - redis
 - postgres
 
Running the application locally:
docker-compose up

The application is CI/CD enabled.
Any changes pushed to the application gets picked up by travis CI, which (as defined in the .travis.yml file)
 - builds a test image (of client) and runs the tests
 - builds the 'prod' images and pushes them to docker hub
 - deploys the app to elastic beanstalk

Elastic beanstalk then (as defined in the Dockerrun.aws.json file) pulls the images from docker hub and runs them.
As we expect the postgres and redis containers to persist outside the lifecycle of EB, we create them with RDS and Elasicache and configure EB to point to them.

