[![Contributors](https://img.shields.io/github/contributors/bcgov/nr-arch-java-quarakus-template)](/../../graphs/contributors)
[![Forks](https://img.shields.io/github/forks/bcgov/nr-arch-java-quarakus-template)](/../../network/members)
[![Stargazers](https://img.shields.io/github/stars/bcgov/nr-arch-java-quarakus-template)](/../../stargazers)
[![Issues](https://img.shields.io/github/issues/bcgov/nr-arch-java-quarakus-template)](/../../issues)
[![MIT License](https://img.shields.io/github/license/bcgov/nr-arch-java-quarakus-template.svg)](/LICENSE.md)
![Lifecycle:Experimental](https://img.shields.io/badge/Lifecycle-Experimental-339999)
# nr-arch-java-quarakus-template
This Repository is a Quarkus template for crud API.
This project uses Quarkus, the Supersonic Subatomic Java Framework.
If you want to learn more about Quarkus, please visit its website: https://quarkus.io/ .

## To Run this in JVM mode on local,
1. if you have maven run: `mvn clean package -Dquarkus.package.type=legacy-jar` after that just run the `docker-compose up` command.
2. if you don't have maven just uncomment line 8 and comment line#7 in Dockerfile and run `docker-compose up` command.

## To Run this in Native mode on local,
1. Please run ` docker-compose  -f docker-compose-native.yaml up --build`

_Once the 3 containers(app, postgres, keycloak) are running, you can access the keycloak at:
http://localhost:8190/auth
enter admin/admin as username and password.
create a client by uploading kc-client.json file in the root of this quarkus-example project.
now you can access the app swagger at:
http://localhost:8000/q/swagger-ui/
As it is secured with KC token , you can call token endpoint of KC to get a token and then pass it on to use API. Click on Authorize button on swagger UI and copy the token . The token expires in 5 minutes, so if 401 is returned , repeat the token fetch process_

Postman sample to get a token:
![img.png](img.png)
If you want to learn more about building native executables, please consult https://quarkus.io/guides/maven-tooling.

## Deployment to openshift
1. follow this link for artifactory knowledge https://developer.gov.bc.ca/Artifact-Repositories-(Artifactory),  it helps in understanding build and push of image to openshift.
2. Create secrets in GitHub
    1. This example repo has 3 secrets which are available for all deployments and then environment specific secrets are for each deployment.
        - `DOCKER_HUB_ACCESS_TOKEN`
        - `DOCKER_HUB_USERNAME`
        - `OPENSHIFT_SERVER`
    2. The quarkus-dev environment has secrets specific to this deployment.
        - `OPENSHIFT_TOKEN` The token to access openshift namespace where this will be deployed ex: `aaaaaa-dev`
        - `OIDC_AUTH_SERVER_URL` The URL of the Keycloak server
        - `NAMESPACE_NO_ENV` The namespace of the deployment ex: `aaaaaa`
3. Please refer to this file for sample openshift deployment. `.github/workflows/openshift-dev-deploy.yaml`
4. This deploys a single pod postgres. For HA needs teams can use patroni or crunchy.
5. The image size produced is around 50 MB.
6. The application starts up within 2 seconds, with 50-150mc cpu and consumes around 35 Megs of memory.
7. The app consumes around .2mc cpu during idle time.

## Related Guides

- RESTEasy JAX-RS ([guide](https://quarkus.io/guides/rest-json)): REST endpoint framework implementing JAX-RS and more
- SmallRye Health ([guide](https://quarkus.io/guides/microprofile-health)): Monitor service health

## Provided Code

### RESTEasy JAX-RS

Easily start your RESTful Web Services

[Related guide section...](https://quarkus.io/guides/getting-started#the-jax-rs-resources)

### SmallRye Health

Monitor your application's health using SmallRye Health

[Related guide section...](https://quarkus.io/guides/smallrye-health)
