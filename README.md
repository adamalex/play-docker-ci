### Use Automated Builds on Docker Hub for easy Continuous Integration of Play Framework projects

The official [Docker Hub](https://hub.docker.com/) provides an [Automated Builds](http://docs.docker.com/docker-hub/builds/) feature for consistent building of Docker images. Another possible use case for this service, which hasn't received as much attention, is Continuous Integration. Simply provide a `Dockerfile` for your project that runs tests during `docker build`. Docker Hub's integration with GitHub and Bitbucket will pick up new commits, run your tests, and generate new Docker images when tests are successful. Further, the service offers [webhooks](http://docs.docker.com/docker-hub/builds/#webhooks), which can be utilized to extend this use case into Continuous Deployment.

### Example files

* `Dockerfile` creates a suitable Java environment for Play Framework, then uses [Typesafe Activator](https://typesafe.com/activator) to test and build the project during image creation.  The image [ENTRYPOINT](http://docs.docker.com/reference/builder/#entrypoint) is set to run the optimized project so `docker run` will default to launching the Play project within the container.  Testing and compilation are performed only once, during image creation, so all generated images are pre-certified and can be deployed and started without rerunning the tests

* The remainder of the files in this repo provide an example Play Framework project that responds to the standard `activator` commands

### Usage

1. Copy `Dockerfile` into any Play Framework project that responds to the standard `activator` commands

1. Update the ADD commands to include all project files needed for testing and running the app

1. To test with a local image, run `docker build --tag="myplayapp" .`

1. To start the local image, run `docker run -i -t -P myplayapp`

1. To use Docker Hub for CI, push the project and its Dockerfile to GitHub or BitBucket and [configure your automated build](http://docs.docker.com/docker-hub/builds/#setting-up-automated-builds-with-github)

1. Consider using the [webhooks](http://docs.docker.com/docker-hub/builds/#webhooks) feature to trigger deployments for successful builds

### Getting In Touch

[Tweet at me](https://twitter.com/adamalex) or [File an issue](https://github.com/adamalex/play-docker-ci/issues)
if you have questions or comments. Suggestions or ideas for improvement are greatly appreciated.
