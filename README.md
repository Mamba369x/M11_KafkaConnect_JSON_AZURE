# Kafka Connect

Link to project repo - https://github.com/Mamba369x/M11_KafkaConnect_JSON_AZURE


## Prerequisites

- Azure CLI
- Terraform
- Python 3
- wget (for Linux/Mac) or PowerShell (for Windows)
- Make

## Environment Variables

Before running the Makefile targets, ensure that the following environment variables are set:

- `TF_VAR_SUBSCRIPTION_ID`: Your Azure subscription ID

### Setting Environment Variables

#### On Mac and Linux

To set the environment variables on Mac or Linux, you can use the `export` command in the terminal:

```bash
export TF_VAR_SUBSCRIPTION_ID=<your_subscription_id>
```

#### On Windows

To set the environment variables on Windows, you can use the `set` command in the Command Prompt or `setx` command for permanent environment variables.

For the current session:

```cmd
set TF_VAR_SUBSCRIPTION_ID=<your_subscription_id>
```

## Example Usage

To run the complete setup and execute the Spark job, use the following commands:

```bash
make start
```

* Step 1: Unzipping and Azure Login
The first step involves unzipping provided data and logging into Azure.
![Step 1:](src/azure_login.png)

## Install Confluent Hub Client

You can find the installation manual [here](https://docs.confluent.io/home/connect/confluent-hub/client.html)

## Create a custom docker image

For running the azure connector, you can create your own docker image. Create your azure connector image and build it.

## Launch Confluent for Kubernetes

### Create a namespace

- Create the namespace to use:

  ```cmd
  kubectl create namespace confluent
  ```

- Set this namespace to default for your Kubernetes context:

  ```cmd
  kubectl config set-context --current --namespace confluent
  ```

### Install Confluent for Kubernetes

- Add the Confluent for Kubernetes Helm repository:

  ```cmd
  helm repo add confluentinc https://packages.confluent.io/helm
  helm repo update
  ```

- Install Confluent for Kubernetes:

  ```cmd
  helm upgrade --install confluent-operator confluentinc/confluent-for-kubernetes
  ```

## Create your own connector's image

- Create your own connector's docker image using provided Dockerfile and use it in confluent-platform.yaml

### Install Confluent Platform

- Install all Confluent Platform components:

  ```cmd
  kubectl apply -f ./confluent-platform.yaml
  ```

- Install a sample producer app and topic:

  ```cmd
  kubectl apply -f ./producer-app-data.yaml
  ```

- Check that everything is deployed:

  ```cmd
  kubectl get pods -o wide 
  ```

### View Control Center

- Set up port forwarding to Control Center web UI from local machine:

  ```cmd
  kubectl port-forward controlcenter-0 9021:9021
  ```

- Browse to Control Center: [http://localhost:9021](http://localhost:9021)

## Create a kafka topic

- The topic should have at least 3 partitions because the azure blob storage has 3 partitions. Name the new topic: "expedia".

## Prepare the azure connector configuration

## Upload the connector file through the API
