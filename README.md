# Boilerplate for nginx with Let’s Encrypt on docker-compose and and a simple Create-react-app application hosted on nginx

This Project is built following this guide [step-by-step guide on how to
set up nginx and Let’s Encrypt with Docker](https://medium.com/@pentacent/nginx-and-lets-encrypt-with-docker-in-less-than-5-minutes-b4b8a60d3a71).

### Follow the modified steps below to get this demo to work instead of the steps given in the tutorial

- Setup a DOCKER droplet on DigitalOcean
- On DigitalOcean, make a A-record using your domain to point to this droplet (in the code test.mydemos.dk is used, REPLACE all occurences as explained below)
- Add port 80 + 443 to the firewall (Test firewall is open via docker run -d -p 80:80 nginx)
- Clone this repository on your new Droplet
- To build the react-code install node using option2 here: https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04

### Navigate into the project folder

- Open `default.conf` and replace ALL (four) occurences of *test.mydemos.dk* with YOUR OWN domain name
- Open `init-letsencrypt.sh` and replace *test.mydemos.dk* with YOUR OWN Domain Name and add a valid email address
- Observe that staging is set to 1. Leave it like that until the script executes OK, and then set it to 0
- Make the script executable --> `sudo chmod +x init-letsencrypt.sh`
- Execute the script --> `sudo ./init-letsencrypt`
- When everything is fine, change *staging* to 0, and run the script agina to create the certificates --> *After that this script should not be run*

### Build the react project
- Navigate into the `reactapp` folder and make the buildscript executable --> `sudo chmod +x buildreactcode.sh`
- run --> `sudo npm install`
- Execute the script `sudo ./buildreactcode.sh`

### Start nginx and the deployed react-project

- Navigate back up to the project folder and run --> `sudo docker-compose up -d`
- Verify that your react site is hosted on your domain name using HTTPS


