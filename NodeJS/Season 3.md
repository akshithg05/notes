
## Deployment on a server - Frontend

We will be using AWS for deploying the application on the server.
- Create free ec2 instance.

- create a key pair and download the .pem file

- store it locally and then change permission of the .pem file "chmod 400 <.pem file>"

- ssh into the ec2 instance using - ssh -i "dev-tinder-frontend-secret.pem" ubuntu@ec2-13-203-195-71.ap-south-1.compute.amazonaws.com

- Install node in the machine and make sure the same working version of the local version is added.

- SSh into machine and clone the backend and frontend projects.

- cd into frontend project, do npm install and create a build - npm run build

- update system - sudo apt update

- install nginx - sudo apt install nginx

- start nginx - sudo systemctl start nginx

- enable nginx - sudo systemctl enable nginx

- Copy code from dist folder (build files) to nginx http server (/var/www/html) - sudo scp -r dist/\* /var/www/html

- Enable port 80 on instance through aws security groups


# Backend

  

- Whitelist the instance IP on mongodb

- Copy .env file to the instance folder where backend app is running.

- Run "npm start" and see if it works.

- Install pm2 (process manager) to keep the connection alive, not rely on terminal - "npm install pm2 -g"

- Run "pm2 start npm -- start" - To start a new process and keep it running online

- For logs - pm2 logs

- clear logs - pm2 flush |name_of_process|

- list of services - pm2 list

- Stop and delete service - pm2 delete |service|

- Custom name to service - pm2 start npm --name "dev-tinder-backend" -- start

- Use nginx proxy pass to map /api to port :3000

- nginx config location - sudo nano /etc/nginx/sites-available/default

  

- nginx config :

  

  server_name 13.203.195.71;

  

        # Proxy API requests to Node.js backend

        location /api/ {

                proxy_pass http://localhost:3000/;

                proxy_http_version 1.1;

                proxy_set_header Upgrade $http_upgrade;

                proxy_set_header Connection 'upgrade';

                proxy_set_header Host $host;

                proxy_cache_bypass $http_upgrade;

        }

  

- We need to restart nginx - sudo systemctl restart nginx

- Modify BASE_URL in front end to /api



## Payment Gateways - 3/11/2035
![[Pasted image 20251103220518.png]]

See notes from book / see from 23 mins of video.