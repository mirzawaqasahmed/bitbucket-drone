# Bitbucket + Drone setup

## Doc

Bitbucket install instructions: https://hub.docker.com/r/atlassian/bitbucket-server/  
Drone install instructions: http://docs.drone.io/install-for-bitbucket-server/  
Drone doc: https://discourse.drone.io/t/bitbucket-server-documentation/176/4  
Webhook plugin: https://github.com/drone/docs/issues/223  

## Install instructions

Tweak docker-compose
- Edit docker-compose to match your available ports and host names
- For this example, I'll keep the dockerfile as-is and add `127.0.0.1 bitbucket` and `127.0.0.1 drone-server`to my hosts file
- Start the stack

Startup bitbucket
- Setup bitbucket, register and shit
- Install the Webhook plugin on bitbucket (see link above)
- Create a project and a repo
- Add a user for drone that matches the creds in docker-compose

Create an application link
- Get into the admin settings and find the "Application Links" section
- Create one with the url http://drone-server/authorize, leave the rest blank
- Click edit on the link that you just made, and add incoming auth settings
- The consumer key is in docker compose
- The consumer name can be anything
- Example keys have been added to this repo. Use the pub key in the `public key` field.
- Set the Consumer Callback URL to http://drone-server/authorize

Connect to drone
- Point your browser to drone-server. Login should work.
- Enable a project
- If you check back in the settings of your repo on bitbucket, you should see that post-recieve webhooks have been enabled by drone.

Get back on your machine
- Add a `.drone.yml` file to your stash repo, and push it
