# Udagram Simple Frontend

Udagram is a simple cloud application developed along side the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.

The project is split into four parts:
1. [The Simple Frontend](frontend)
A basic Ionic client web application which consumes the RestAPI Backend. 
2. [The Feed RestAPI Backend](restapi-feed), a Node-Express server which can be deployed to a cloud service.
3. [The User RestAPI Backend](restapi-user), a Node-Express server which can be deployed to a cloud service.
4. [The Proxy to redirect each RestAPI](proxy), nginx config.
***

## Getting Setup

### Installing Node and NPM
This project depends on Nodejs and Node Package Manager (NPM). Before continuing, you must download and install Node (NPM is included) from [https://nodejs.com/en/download](https://nodejs.org/en/download/).

### Installing Ionic Cli
The Ionic Command Line Interface is required to serve and build the frontend. Instructions for installing the CLI can be found in the [Ionic Framework Docs](https://ionicframework.com/docs/installation/cli).

### Installing project dependencies

This project uses NPM to manage software dependencies. NPM Relies on the package.json file located in the root of this repository. After cloning, open your terminal and run:
```bash
npm install
```
>_tip_: **npm i** is shorthand for **npm install**

### Configure The Backend Endpoint
Ionic uses enviornment files located in `./src/enviornments/enviornment.*.ts` to load configuration variables at runtime. By default `environment.ts` is used for development and `enviornment.prod.ts` is used for produciton. The `apiHost` variable should be set to your server url either locally or in the cloud.

***
### Running the Development Server
Ionic CLI provides an easy to use development server to run and autoreload the frontend. This allows you to make quick changes and see them in real time in your browser. To run the development server, open terminal and run:

```bash
ionic serve
```

### Building the Static Frontend Files
Ionic CLI can build the frontend into static HTML/CSS/JavaScript files. These files can be uploaded to a host to be consumed by users on the web. Build artifacts are located in `./www`. To build from source, open terminal and run:
```bash
ionic build
```
***

## Deployment
In addition project contains the `deployment` dir which contains all required scripts to build docker images and deploy them using docker or kubernetes.
You'll be required to add on your own the following env config for kubernetes.

### AWS secret credentials

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: aws-secret
type: Opaque
data:
  credentials: <base64_encoded_credentials>
```

### ENV secret

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: env-secret
type: Opaque
data:
  DB_USER: <base64_encoded_db_user>
  DB_PASSWORD: <base64_encoded_db_password>
```

### ENV secret

```yaml
apiVersion: v1
kind: ConfigMap
data:
  AWS_BUCKET: <aws_bucket>
  AWS_PROFILE: <aws_profile>
  AWS_REGION: <aws_region>
  JWT_SECRET: <some_secret>
  DB_NAME: <aws_rds_db_name>
  DB_HOST: <aws_rds_host>
  DB_DIALECT: postgres
  URL: http://localhost:8100  
metadata:
  name: env-config
```