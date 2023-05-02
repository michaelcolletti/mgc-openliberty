

- Create the Docker container using the OpenLiberty Image

```
FROM openliberty/open-liberty:latest
COPY --chown=1001:0 src/main/liberty/config/server.xml /config/
COPY --chown=1001:0 target/your-application.war /config/apps/
RUN configure.sh
```
-Build the code
```
docker build -t your-image-name:your-tag .

```
- Push to CR

```
docker push your-docker-hub-username/your-image-name:your-tag
```
- Deploy to OpenShift 

```
oc login -u your-openshift-username -p your-openshift-password https://your-openshift-cluster-url
oc new-project your-project-name
oc new-app your-docker-hub-username/your-image-name:your-tag
oc expose service/your-app-name
```


