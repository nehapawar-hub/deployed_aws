# Travel Memory Application Deployment on AWS EC2

## 1. Introduction

The Travel Memory application is a full-stack web application built using the MERN stack. This project demonstrates deployment of the React frontend and Node.js/Express backend on Amazon EC2, database connectivity using MongoDB Atlas, traffic distribution using an AWS Application Load Balancer, and custom-domain configuration through Cloudflare.

## 2. Project Objectives

* Deploy the backend on Node.js.
* Configure the React frontend.
* Connect the frontend to the backend API.
* Configure Nginx as a web server and reverse proxy.
* Deploy multiple application instances.
* Configure an AWS Application Load Balancer.
* Connect the application to a custom domain through Cloudflare.
* Document the deployment process and validate the application.

## 3. Technologies Used

* React.js
* Node.js
* Express.js
* MongoDB Atlas
* Amazon EC2
* Nginx
* AWS Application Load Balancer
* AWS Certificate Manager
* Cloudflare DNS
* Git and GitHub
* diagrams.net

## 4. Repository Setup

Source repository:
https://github.com/UnpredictablePrashant/TravelMemory

The repository was cloned onto the EC2 instance. The frontend and backend directories were inspected to identify their dependencies, entry points, environment variables, and startup commands.

Screenshot: `Screenshots/01-github-repository.png`

## 5. EC2 Configuration

An Ubuntu EC2 instance was launched with the required networking and security-group settings. SSH access was restricted to the administrator's IP address, and public HTTP/HTTPS access was configured as required.

Screenshot: `Screenshots/02-ec2-instance.png`

## 6. Backend Configuration

The backend dependencies were installed using npm. A `.env` file was configured with the backend port and MongoDB connection details. The backend was configured to listen on port 3000.

The backend was run as a systemd service so that it could start automatically after a restart.

Screenshot: `Screenshots/06-backend-running.png`

## 7. Frontend Configuration

The React frontend dependencies were installed. The API URL configuration was updated to use the deployed backend endpoint or the relative API path routed by Nginx. The production build was generated and deployed to the Nginx web root.

Screenshot: `Screenshots/07-frontend-running.png`

## 8. Nginx Reverse Proxy

Nginx was configured to serve the React production build and forward API requests to the Node.js backend. The Nginx configuration was tested before being reloaded.

Screenshot: `Screenshots/08-api-communication.png`

## 9. Database Configuration

MongoDB Atlas was configured with an application database user and suitable network-access restrictions. The backend connection was tested without exposing credentials in the repository or screenshots.

Screenshot: `Screenshots/05-mongodb-atlas.png`

## 10. Load Balancer Configuration

An AWS Application Load Balancer was created. Frontend and backend targets were registered in the appropriate target groups, and health checks were configured.

Screenshot: `Screenshots/09-load-balancer.png`

## 11. HTTPS Configuration

An SSL/TLS certificate was requested and validated using AWS Certificate Manager. An HTTPS listener was configured on the load balancer.

Screenshot: `Screenshots/11-https-configuration.png`

## 12. Cloudflare DNS Configuration

Cloudflare DNS records were configured to route the custom domain to the application load balancer. Any required EC2 A record was configured separately according to the assignment requirements.

Screenshot: `Screenshots/12-cloudflare-dns.png`

## 13. Architecture Diagram

The deployment architecture diagram illustrates the flow from the user and custom domain through Cloudflare and the AWS load balancer to the frontend and backend instances and MongoDB Atlas.

Files:

* `Architecture/TravelMemory-Deployment-Architecture.drawio`
* `Architecture/TravelMemory-Deployment-Architecture.png`

## 14. Testing and Validation

The deployment was validated by checking frontend accessibility, backend service status, API responses, database connectivity, load-balancer target health, DNS resolution, and HTTPS availability.

Screenshot: `Screenshots/13-final-application.png`

## 15. Security Considerations

* Sensitive credentials were kept out of source control.
* SSH access was restricted to an authorized IP address.
* Backend access was restricted to authorized traffic sources.
* MongoDB Atlas network access was limited as appropriate.
* HTTPS was configured for public access.
* Database credentials and private keys were not included in screenshots or documentation.

## 16. Conclusion

The Travel Memory application was deployed using AWS EC2, with Nginx serving the frontend and forwarding API requests to the Node.js backend. MongoDB Atlas provided managed database services, an Application Load Balancer distributed traffic across multiple targets, and Cloudflare DNS connected the custom domain to the application.
