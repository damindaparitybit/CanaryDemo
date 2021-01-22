# Color application
This applications displays a blank webpage with a color retrieved from the backend. It can also display the number of times a certain color is shown. This application is designed to showcase two different deployment strategies: blue-green deployments and canary deployments. The app is written in Rustlang because the author wanted to take a look at it.

## Deployment
The deployment has to separate components, a frontend components and a backend component. The frontend has a simple website that displays a single color. The color is determined by a call to the backend that returns the displayed color in a short JSON message. Both the frontend and the backend listen by default on port 8000. The frontend can also the ratio of backend color results, which can be used to visualize deployment updates and the behavour of successding and failing canary deployments.

Both the frontend and the backend require the APIKey environment variable to be set in order to make calls. The backend additionally needs a configmap mounted into the following path: "/config/config.yaml". The config file can be found in the backend/config folder and can be used as a reference.

The backend has an additional health endpoint under /health that can be used for liveness and readiness probes. Whether the healthchecks fail or not can be determined by the confiig file.

### Tips

- Create an api secret and make it available as env var
- Create a config map based on backend/config/config.yaml and mount it to /config/config.yaml
- Expose port 8000 on both components and create a matching service

## Version Branches
Each branch represents a separate version of the canary demo. The version 1.0 will display a simple website blue website, v1.1 will cause a 500 range error and v1.2 will result in  a green website. This is only used to demonstrate and test canary deployments.

## Tasks
1) Optionally: Fork the repo, build automated docker images for the frontend and backend components, use github tags for image building
2) Create service and deployment manifest along with additional required manifests (configmap/secret) for the frontend and backend component and deploy them
3) Create ingress yaml for frontend component and deploy it
4) Check if the website if working