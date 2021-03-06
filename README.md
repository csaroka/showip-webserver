# lbtest-websvr

Continer image with Apache and PHP that echos the running instance's current IP address on the main page.

`git clone https://github.com/csaroka/lbtest-websvr.git`\
`cd lbtest-websvr`

#### Build in Docker or Pull Pre-Built Image
`docker build -t lbtest-websvr .` \
Alternatively, pull the pre-built image: \
`docker pull csaroka/showmeip:lts`

#### Run in Docker
`docker run -p 8080:80 -d lbtest-websvr`

#### Verify instance is reporting IP
`curl localhost:8080`

#### Stop the instance
`docker stop <Container-ID>`

#### Ship to a private registry
`docker tag lbtest-websvr harbor.lab.local/library/lbtest-websvr:v1` \
`docker push harbor.lab.local/library/lbtest-websvr:v1`

#### Create deployment on Kubernetes cluster
`kubectl run lbtest-websvr --image=harbor.lab.local/library/lbtest-websvr:v1 --replicas=4 --port=80`

#### Attach a LoadBalancer service to the deployment
`kubectl expose deployment lbtest-websvr--port=80 --type=LoadBalancer`

#### Get service External IP
`kubectl get svc`

#### Verify Load-balancing
`curl -w "\n" http://<External-IP>`
