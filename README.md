# Deploying a Flask API

This is the project starter repo for the fourth course in the [Udacity Full Stack Nanodegree](https://www.udacity.com/course/full-stack-web-developer-nanodegree--nd004): Server Deployment, Containerization, and Testing.

In this project you will containerize and deploy a Flask API to a Kubernetes cluster using Docker, AWS EKS, CodePipeline, and CodeBuild.

The Flask app that will be used for this project consists of a simple API with three endpoints:

- `GET '/'`: This is a simple health check, which returns the response 'Healthy'. 
- `POST '/auth'`: This takes a email and password as json arguments and returns a JWT based on a custom secret.
- `GET '/contents'`: This requires a valid JWT, and returns the un-encrpyted contents of that token. 

The app relies on a secret set as the environment variable `JWT_SECRET` to produce a JWT. The built-in Flask server is adequate for local development, but not production, so you will be using the production-ready [Gunicorn](https://gunicorn.org/) server when deploying the app.

## Initial setup
1. Fork this project to your Github account.
2. Locally clone your forked version to begin working on the project.

## Dependencies

- Docker Engine
    - Installation instructions for all OSes can be found [here](https://docs.docker.com/install/).
    - For Mac users, if you have no previous Docker Toolbox installation, you can install Docker Desktop for Mac. If you already have a Docker Toolbox installation, please read [this](https://docs.docker.com/docker-for-mac/docker-toolbox/) before installing.
 - AWS Account
     - You can create an AWS account by signing up [here](https://aws.amazon.com/#).
     

## Storing Environment variables

Create a file named `.env_file` and save both `JWT_SECRET` and `LOG_LEVEL` into `.env_file`. 
These environment variables will run locally in your container. 
Here, we do not need the export command, just an equals sign:

` JWT_SECRET='myjwtsecret'`
` LOG_LEVEL=DEBUG`

This `.env_file` is only for the purposes of running the container locally, you do not want to push it into the Github or other public repositories. 
You can prevent this by adding it to your `.gitignore `file, which will cause git to ignore it. 
To safely store and use secrets in the cloud, use a secure solution such as AWS’s parameter store.


## Project Steps

Completing the project involves several steps:

1. Write a Dockerfile for a simple Flask API
2. Build and test the container locally
3. Create an EKS cluster
4. Store a secret using AWS Parameter Store
5. Create a CodePipeline pipeline triggered by GitHub checkins
6. Create a CodeBuild stage which will build, test, and deploy your code

For more detail about each of these steps, see the project lesson [here](https://classroom.udacity.com/nanodegrees/nd004/parts/1d842ebf-5b10-4749-9e5e-ef28fe98f173/modules/ac13842f-c841-4c1a-b284-b47899f4613d/lessons/becb2dac-c108-4143-8f6c-11b30413e28d/concepts/092cdb35-28f7-4145-b6e6-6278b8dd7527).


## Stop EKS cluster to avoid costs

If no production you can stop your machine as below: 
1. [This](https://stackoverflow.com/a/68586990/7694643)
2. [Or this](https://stackoverflow.com/a/55372140/7694643)

Go to EC2 instances dashboard of your Node Group and from right panel in bottom click on Auto Scaling Groups then select your group by click on checkbox and click edit button and change Desired, Min & Max capacities to 0 (before all are 2).
![img.png](img.png)