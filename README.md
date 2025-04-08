2048 Game on AWS Elastic Beanstalk
This repository demonstrates how to deploy the 2048 game on AWS Elastic Beanstalk using Docker. The application is containerized using a custom Docker image, which installs Nginx, downloads the game, and serves it through a web server.

🚀 Deployment Steps
1. Create a Repository on GitHub
Created a repository on GitHub to store the project files.

2. Clone the Repository to Your Computer
Clone the repository to your local machine using the following command on  WIndows powershell:

git clone git@github.com:Hajixhayjhay/2048-games.git

3. Open the Repository in Visual Studio Code
Open the cloned repository in Visual Studio Code to start working on the project.

4. Create the Dockerfile
In the Visual Studio Code, create a Dockerfile in the root directory of the project and add the following content:

# Use Ubuntu 22.04 as the base image
FROM ubuntu:22.04

# Update package list and install Nginx, zip, and curl
RUN apt-get update
RUN apt-get install -y nginx zip curl

# Ensure Nginx runs in the foreground (without daemonizing)
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

# Download the 2048 game from GitHub
RUN curl -o /var/www/html/master.zip -L https://codeload.github.com/gabrielecirulli/2048/zip/master

# Unzip the downloaded game, move files to the correct location, and clean up
RUN cd /var/www/html && unzip master.zip && mv 2048-master/* . && rm -rf 2048-master master.zip

# Expose port 80 for web traffic
EXPOSE 80

# Run Nginx in the foreground with the specified configuration
CMD ["/usr/sbin/nginx", "-c", "/etc/nginx/nginx.conf"]
5. Deploy to AWS Elastic Beanstalk
a. Create an Application in the Elastic Beanstalk Console
Go to the Elastic Beanstalk console on AWS.

Create a new application and configure the environment.

b. Configure the Environment
Select the Docker platform.

Upload the Dockerfile from your local machine as the application code.

c. Configure the Presets and Service Access
Set up the service role and EC2 instance profile for the application.

Leave other configurations as default and skip any optional steps.

d. Create the Environment
After configuring the environment, click Create to create the Elastic Beanstalk environment.

6. Access the 2048 Game
Once the environment is created, you will be provided with a domain name.

Use the provided domain name to access the 2048 game running on AWS.

📚 Additional Information
Docker was used to containerize the 2048 game, ensuring consistent environment across local and cloud deployments.

Nginx serves the game through port 80.

AWS Elastic Beanstalk handles the environment management, scaling, and monitoring.


