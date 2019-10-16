# Community Node Service Configuration and Deployment

**Version: 0.2.0**

## Description

The Community Node Service is the content manager for the Community Node and its associated Access Nodes. It exports two resources: the Community Node's home webpage and an info API endpoint. 

## Community Node Reference Service

A reference CN Service, written as a NodeJS server with Express, is available to use as a framework for building out additional capabilities. 

Note that using this specific implementation is not a requirement; the reference service is a suggestion only. 

[GitHub Repository for Community Node Source](https://github.com/opespe/cn-service-reference.git)

### Prerequisites

- [NodeJS Version 10 LTS](https://nodejs.org/en/)
- [Node Package Manager](https://www.npmjs.com/) (Distributed with NodeJS)

### Local Deployment Process 

This process deploys the refernce Community Node Service. If you have an existing web server, see the instructions below. 

### Configuration

Follow these steps to configure the reference CN Service on the local machine. 

#### 1. Edit Info

Modify the `/data/info.json` file to use your desired values according to the [Community Node Service Info Spec](./community_info_spec.md)

#### 2. Edit Landing Page

Modify the `/data/index.html` file to display your desired landing page.

#### 3. Edit Icon

Modify the `/data/icon.png` file to display your desired avatar icon. 

**Note:** The icon size should be 120px by 120px. The file should be a PNG.

**Note:** If you are running behind a proxy the app will try to resolve the host using the `X-Forwarded-Host` header of the request. If this does not work in your environment you may need to explicitly define the icon url in the **info.json**. For example, given the Community Node's FQDN is `example-cn.com` the value for the icon key would be set to `https://example-cn.com/icon.png`).

#### 4. Install and Run

Run
```
npm install
npm start
```

After this step, the Community Node software should be running on port `8080`. Consult the local system administrator to make the port externally accessible.

Note that a Dockerfile is also provided for use in a containerized environment.


## Integration with Existing Servers

If you have an existing web server, you may simply add the info endpoint to the server. The endpoint may be at any location, but it must be externally accessible. This endpoint must be the same one submitted during account creation.

### Endpoint Specification

**HTTP Method**: GET

**Return Content-Type**: application/json

#### Return Object

The endpoint should return a JSON object with the proper field names and values according to the [Community Node Service Info Spec](./community_info_spec.md). These fields will be visible to Personal Nodes through the mobile app when they are exploring communities. 
