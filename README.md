# Deploy-API-server-in-K8s

Here, I have exposed my HTTP-API-server https://github.com/Neaj-Morshad-101/HTTP-API-server
by creating a NodePort type service.

Steps to follow to run this API server: 

### Step 01: Create the deployment and the service using the following commands
`kubectl apply -f http-api-server-deployment.yaml`

`kubectl apply -f http-api-server-service.yaml`

### Step 02: To know your node's ip 
`kubectl get node -o wide`

Now you have found your node's ip (INTERNAL-IP)
In my case, It is 172.18.0.2

As the service is exposed at NodePort 30000, You can access server on http://172.18.0.2:30000

## Step 03: Now hit the api server using the login info:
curl -X POST -d '{"username":"Neaj Morshad","password":"1234"}' hhttp://172.18.0.2:30000/login

Notes: You can do it from the postman also, select verb POST and hit http://172.18.0.2:30000/login in the body section: select raw and the these login data in json format

{ "username" : "Neaj Morshad", "password" : "1234" }

## Step 04: Set the token from the command line using the following command:
TOKEN="eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOlsiTmVhaiBNb3JzaGFkIl0sImV4cCI6MTY3OTY0MjIxOX0.RMoAGj7KGFUtvq3ebpg_3ksQJqy4Q-gA5jAfOF4SCPQ"

Notes: You will find this token in response section (Cookies) in Posman. Name: jwt Value: TOKEN For the posman you don’t have to set any thing. Go to bash, bacause ‘=’ is not supported in fish

Step 05: Now hit the API sever using any commands like this:
curl -H 'Accept: application/json' -H "Authorization: Bearer ${TOKEN}" http://localhost:8080/albums

Notes: You can hit the API using postman also, Select correct verb and the API endpoints (GET, PUT, POST, DELETE)





In case you need help regarding NodePort type service, 
You can find some theories of NodePort type service here: https://github.com/Superm4n97/kubernetes/tree/main/Kubernetes%20Resources/Services