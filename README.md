# Udagram Image Filtering Microservice

Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.

The project is split into three parts:
1. [The Simple Frontend](https://github.com/udacity/cloud-developer/tree/master/course-02/exercises/udacity-c2-frontend)
A basic Ionic client web application which consumes the RestAPI Backend. [Covered in the course]
2. [The RestAPI Backend](https://github.com/udacity/cloud-developer/tree/master/course-02/exercises/udacity-c2-restapi), a Node-Express server which can be deployed to a cloud service. [Covered in the course]
3. [The Image Filtering Microservice](https://github.com/udacity/cloud-developer/tree/master/course-02/project/image-filter-starter-code), the final project for the course. It is a Node-Express application which runs a simple script to process images. [Your assignment]

## Github repo URL
https://github.com/mwd19/image-filter-final-code

## Endpoint URL for the running elastic beanstalk deployment (EB_URL) 
http://image-filter-final-code-dev.us-east-1.elasticbeanstalk.com/

### Valid GET request
http://image-filter-final-code-dev.us-east-1.elasticbeanstalk.com/filteredimage?image_url=https://upload.wikimedia.org/wikipedia/commons/7/73/Lion_waiting_in_Namibia.jpg

## Tasks

### Setup Node Environment

You'll need to create a new node server. Open a new terminal within the project directory and run:

1. Initialize a new project: `npm i`
2. run the development server with `npm run dev`

``` bash
➜  image-filter-final-code git:(dev) npm run dev  

> udacity-c2-image-filter@1.0.0 dev
> ts-node-dev ./src/server.ts

Using ts-node version 8.3.0, typescript version 3.5.3
server running http://localhost:8082
press CTRL+C to stop server
```

### Create a new endpoint in the server.ts file

The starter code has a task for you to complete an endpoint in `./src/server.ts` which uses query parameter to download an image from a public URL, filter the image, and return the result.

We've included a few helper functions to handle some of these concepts and we're importing it for you at the top of the `./src/server.ts`  file.

```typescript
import {filterImageFromURL, deleteLocalFiles} from './util/util';
```

### Deploying your system
Follow the process described in the course to `eb init` a new application and `eb create` a new environment to deploy your image-filter service! Don't forget you can use `eb deploy` to push changes.

#### `1. npm run build` 
``` bash
➜  image-filter-final-code git:(master) npm run build

> udacity-c2-image-filter@1.0.0 build
> npm run clean && tsc && cp package.json www/package.json && mkdir www/tmp/ && cd www && zip -r Archive.zip . && cd ..


> udacity-c2-image-filter@1.0.0 clean
> rimraf www/ || true

  adding: util/ (stored 0%)
  adding: util/util.js (deflated 62%)
  adding: util/util.js.map (deflated 57%)
  adding: server.js (deflated 62%)
  adding: server.js.map (deflated 62%)
  adding: package.json (deflated 54%)
  adding: tmp/ (stored 0%)
```

#### `2. eb init` 
``` bash
➜  image-filter-final-code git:(master) ✗ eb init                                       

Select a default region
1) us-east-1 : US East (N. Virginia)
2) us-west-1 : US West (N. California)
3) us-west-2 : US West (Oregon)
4) eu-west-1 : EU (Ireland)
5) eu-central-1 : EU (Frankfurt)
6) ap-south-1 : Asia Pacific (Mumbai)
7) ap-southeast-1 : Asia Pacific (Singapore)
8) ap-southeast-2 : Asia Pacific (Sydney)
9) ap-northeast-1 : Asia Pacific (Tokyo)
10) ap-northeast-2 : Asia Pacific (Seoul)
11) sa-east-1 : South America (Sao Paulo)
12) cn-north-1 : China (Beijing)
13) cn-northwest-1 : China (Ningxia)
14) us-east-2 : US East (Ohio)
15) ca-central-1 : Canada (Central)
16) eu-west-2 : EU (London)
17) eu-west-3 : EU (Paris)
18) eu-north-1 : EU (Stockholm)
19) eu-south-1 : EU (Milano)
20) ap-east-1 : Asia Pacific (Hong Kong)
21) me-south-1 : Middle East (Bahrain)
22) af-south-1 : Africa (Cape Town)
(default is 3): 1


Enter Application Name
(default is "image-filter-final-code"): 
Application image-filter-final-code has been created.

It appears you are using Node.js. Is this correct?
(Y/n): 
Select a platform branch.
1) Node.js 14 running on 64bit Amazon Linux 2
2) Node.js 12 running on 64bit Amazon Linux 2
3) Node.js 10 running on 64bit Amazon Linux 2 (Deprecated)
4) Node.js running on 64bit Amazon Linux (Deprecated)
(default is 1): 2

Do you wish to continue with CodeCommit? (Y/n): n
Do you want to set up SSH for your instances?
(Y/n): 

Select a keypair.
1) aws-eb
2) vockey
3) [ Create new KeyPair ]
(default is 2): 1
```

#### `3. eb create` 
``` bash
➜  image-filter-final-code git:(master) ✗ eb create
Enter Environment Name
(default is image-filter-final-code-dev): 
Enter DNS CNAME prefix
(default is image-filter-final-code-dev): 

Select a load balancer type
1) classic
2) application
3) network
(default is 2): 


Would you like to enable Spot Fleet requests for this environment? (y/N): 
Uploading image-filter-final-code/app-ec23-211004_191637.zip to S3. This may take a while.
Upload Complete.
Environment details for: image-filter-final-code-dev
  Application name: image-filter-final-code
  Region: us-east-1
  Deployed Version: app-ec23-211004_191637
  Environment ID: e-zfmqmsnepx
  Platform: arn:aws:elasticbeanstalk:us-east-1::platform/Node.js 12 running on 64bit Amazon Linux 2/5.4.6
  Tier: WebServer-Standard-1.0
  CNAME: image-filter-final-code-dev.us-east-1.elasticbeanstalk.com
  Updated: 2021-10-04 18:16:44.838000+00:00
Printing Status:
2021-10-04 18:16:43    INFO    createEnvironment is starting.
2021-10-04 18:16:45    INFO    Using elasticbeanstalk-us-east-1-927852435336 as Amazon S3 storage bucket for environment data.
2021-10-04 18:17:07    INFO    Created target group named: arn:aws:elasticloadbalancing:us-east-1:927852435336:targetgroup/awseb-AWSEB-JW0GOZ27ENRF/9a13673d9aed9a5b
2021-10-04 18:17:07    INFO    Created security group named: sg-072decac261b9c04b
2021-10-04 18:17:23    INFO    Created security group named: awseb-e-zfmqmsnepx-stack-AWSEBSecurityGroup-1EC7YO2Q82BHL
2021-10-04 18:17:23    INFO    Created Auto Scaling launch configuration named: awseb-e-zfmqmsnepx-stack-AWSEBAutoScalingLaunchConfiguration-1D77KIJGCU0AC
2021-10-04 18:18:25    INFO    Created Auto Scaling group named: awseb-e-zfmqmsnepx-stack-AWSEBAutoScalingGroup-1L7214MPYYNHB
2021-10-04 18:18:25    INFO    Waiting for EC2 instances to launch. This may take a few minutes.
2021-10-04 18:18:25    INFO    Created Auto Scaling group policy named: arn:aws:autoscaling:us-east-1:927852435336:scalingPolicy:30e630bf-c1c3-442d-b483-1b96dcd244e9:autoScalingGroupName/awseb-e-zfmqmsnepx-stack-AWSEBAutoScalingGroup-1L7214MPYYNHB:policyName/awseb-e-zfmqmsnepx-stack-AWSEBAutoScalingScaleDownPolicy-1MN6YAP5QIB49
2021-10-04 18:18:25    INFO    Created Auto Scaling group policy named: arn:aws:autoscaling:us-east-1:927852435336:scalingPolicy:75254470-f7b5-43cd-9d92-b4fd545907a8:autoScalingGroupName/awseb-e-zfmqmsnepx-stack-AWSEBAutoScalingGroup-1L7214MPYYNHB:policyName/awseb-e-zfmqmsnepx-stack-AWSEBAutoScalingScaleUpPolicy-LXO58J0TFE24
2021-10-04 18:18:40    INFO    Created CloudWatch alarm named: awseb-e-zfmqmsnepx-stack-AWSEBCloudwatchAlarmLow-1EJCOZ61D49RO
2021-10-04 18:18:40    INFO    Created CloudWatch alarm named: awseb-e-zfmqmsnepx-stack-AWSEBCloudwatchAlarmHigh-1SYISUEFAIH5M
2021-10-04 18:18:44    INFO    Created load balancer named: arn:aws:elasticloadbalancing:us-east-1:927852435336:loadbalancer/app/awseb-AWSEB-FQOFD5H8V5UJ/d41f1009d87eaa09
2021-10-04 18:18:59    INFO    Created Load Balancer listener named: arn:aws:elasticloadbalancing:us-east-1:927852435336:listener/app/awseb-AWSEB-FQOFD5H8V5UJ/d41f1009d87eaa09/1a6b91a798174a49
2021-10-04 18:19:03    INFO    Instance deployment: You didn't specify a Node.js version in the 'package.json' file in your source bundle. The deployment didn't install a specific Node.js version.
2021-10-04 18:19:20    INFO    Instance deployment completed successfully.
2021-10-04 18:19:54    INFO    Application available at image-filter-final-code-dev.us-east-1.elasticbeanstalk.com.
2021-10-04 18:19:54    INFO    Successfully launched environment: image-filter-final-code-dev
```

## Stand Out (Optional)

### Refactor the course RESTapi

If you're feeling up to it, refactor the course RESTapi to make a request to your newly provisioned image server.

I have give it a try .. but I have a little problem with the uploaded image it gives me an error when I download it, I think that I have not been able to upload it in the correct format.

#### Here is the github repo :
https://github.com/mwd19/udacity-c2-restapi

#### Endpoint URL for the running elastic beanstalk
http://udagram-walid-dev-dev.us-east-1.elasticbeanstalk.com


### Authentication

Prevent requests without valid authentication headers.
> !!NOTE if you choose to submit this, make sure to add the token to the postman collection and export the postman collection file to your submission so we can review!

#### The postman collection
https://github.com/mwd19/udacity-c2-restapi/blob/master/udacity-c2-restapi-dup.postman_collection.json

But I got this error in the response body:
<html>

<head>
	<title>502 Bad Gateway</title>
</head>

<body>
	<center>
		<h1>502 Bad Gateway</h1>
	</center>
	<hr>
	<center>nginx/1.20.0</center>
</body>

</html>

### Custom Domain Name

Add your own domain name and have it point to the running services (try adding a subdomain name to point to the processing server)
> !NOTE: Domain names are not included in AWS’ free tier and will incur a cost.
