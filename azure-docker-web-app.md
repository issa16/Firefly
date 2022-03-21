# Build, Run and Continously Deploy Docker Containers to Azure App Service

### Create a resource
---
- Login to the **[Azure portal](https://portal.azure.com/#home)**
- Click **[Create a resource](https://portal.azure.com/#create/hub)**
- Select the **Containers** tab under **Categories** and click on **Container Registry**
- Complete the **Create container registry** form
  - Subscription: *Azure subscription 1* (default)
  - Resource group: *Docker_Web_App_Demo*
  - Registry name: *issa16*
  - Location: East *US* (default)
  - SKU: *Standard* (default)
- Click **Review + create**
- Click **Create**
- Wait for the deployment to complete
- Click **Go to resource**
- Select the **Access keys** tab under **Settings**
- Enable the **Admin user** option

### Build the Docker image
---
- Obtain the GitHub repo URL
  - Flask Docker Demo: https://github.com/issa16/flask-docker-demo.git
- Clone onto local machine
  - `git clone https://github.com/issa16/flask-docker-demo.git`
- Build a docker image
  - `cd flask-docker-demo`
  - `docker build -t issa16.azurecr.io/flask-docker-demo:latest .`

### Push the Docker image to Azure
---
- Docker login to the fully qualified domain name created in Azure
  - `docker login issa16.azurecr.io`
    - Username: issa16
    - Password is available from the Azure portal under the **Access keys** tab.
- Push the image to Azure
  - `docker push issa16.azurecr.io/flask-docker-demo:latest`

### Build the web app
---
- Within the Azure portal, click **[Create a resource](https://portal.azure.com/#create/hub)**
- Select the **Web** tab under **Categories**
- Search for **Web App for Containers**
- Click **Create**
- Complete the **Create Web App** form
  - Subscription: *Azure subscription 1* (default)
  - Resource Group: *Docker_Web_App_Demo*
  - Name: *flask-docker-demo*
  - Publish: *Docker Container* (default)
  - Operating System: *Linux* (default)
  - Region: *Central US* (default)
  - Linux Plan: *ASP-DockerWebAppDemo* (default)
- Select the **Docker** tab
- Complete the **Docker** form
  - Options: *Single Container* (default)
  - Image Source: *Azure Container Registry*
  - Registry: *issa16*
  - Image: *flask-docker-demo*
  - Tag: *latest*
- Click **Review + create**
- Click **Create**
- Wait for the deployment to complete
- Click **Go to resource**
- Click the URL to test the web app is working
  - https://flask-docker-demo.azurewebsites.net

### Continuous Deployment
---
- Select the **Deployment Center** tab under **Deployment**
- Enable the **Continuous Deployment** option
- Click **Save**
