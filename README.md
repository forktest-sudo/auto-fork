# Auto Fork

`Auto Fork` is a Python Flask app that forks it's own repository to the users account.
The app uses a GitHub OAuth app to service authentication. 
Once authentication is complete the user can click a button to fork the code base into their github account.

[Click here to try out the service running Elastic Beanstalk!](http://auto-fork.us-east-1.elasticbeanstalk.com) 

# Rationale



# Tests

# Run locally

Before running locally, you will need a GitHub OAuth app. [Learn more about setting one up here.](https://docs.github.com/en/developers/apps/creating-an-oauth-app)

1. Configure the GitHub OAuth 
    * Homepage URL: http://localhost:5000/
    * Authorization callback URL: http://localhost:5000/auth
1. In a terminal cd to the project directory
1. `touch .env`
1. `vi .env` and add the following lines 
    * export AF_CLIENT_ID=your_client_id
    * export AF_CLIENT_SECRET=your_client_secret
1. `docker build . -t autofork`
1. `docker run -d -p 5000:5000 --env-file .env autofork`

# Deployment 

Auto Fork is deployed to elastic beanstalk Docker runtime with the EB manifest file in the deploy folder.

1. Create an EB environment utilizing the Docker platform
1. Upload manifest `deploy/Dockerrun.aws.json`
1. Configure environment variables for AF_CLIENT_ID and AF_CLIENT_SECRET  

# Build

Builds are handled by DockerHub. On commit to master, the image builds and is tagged with `latest`. Final image resides at `kyrick/autofork`

You can build locally by running `docker build . -t autofork` in the project directory.

[Click here to view Auto Fork in DockerHub](https://hub.docker.com/r/kyrick/autofork)

# Configuration

```
Important
AF_SECRET_KEY: Flask session secret key. This is important and must be set per environment.
AF_CLIENT_ID: GitHub OAuth app client ID (get this from GitHub)
AF_CLIENT_SECRET: GitHub OAuth app client secret (get this from GitHub)

Optional
AF_FORK_ENDPOINT: Public repo to be forked. Format: https://api.github.com/repos/:user-name/:repo-name/forks
AF_AUTH_ENDPOINT: The GitHub endpoint for OAuth app Authorization
AF_TOKEN_ENDPOINT: The GitHub endpoint for user Access Tokens after Authorization has been granted 
```

