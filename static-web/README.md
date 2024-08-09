## Deploying a Static Website to AWS EC2 with Nginx

### Prerequisites
* An AWS account with access to EC2 and IAM services
* Basic understanding of Linux commands and SSH
* A text editor for creating the website files (HTML and CSS)

### Steps

#### 1. Create an AWS EC2 Instance
* Launch an EC2 instance using your preferred Amazon Machine Image (AMI), such as Ubuntu Server.
* Choose an appropriate instance type based on your expected website traffic.
* Configure a security group to allow incoming traffic on port 80 (HTTP).
* Create a key pair for SSH access.

#### 2. Connect to the Instance
* Use an SSH client (e.g., PuTTY) to connect to your EC2 instance using the private key you created.

#### 3. Update and Install Nginx
```bash
sudo apt update
sudo apt install nginx
```

#### 4. Create a Directory for Your Website
```bash
mkdir mywebsite
```

#### 5. Create Website Files
* Create two files named `index.html` and `styles.css` inside the `mywebsite` directory.
* Add the following content to `index.html`:
```html
<!DOCTYPE html>
<html>
<head>
  <title>My Personal Project</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <h1>This is My Personal Project</h1>
  <p>Created by Victor Okonkwo</p>
</body>
</html>
```
* Add the following content to `styles.css`:
```css
body {
  font-family: Arial, sans-serif;
  text-align: center;
  background-color: #f2f2f2; /* Light gray background */
}

h1 {
  color: #3498db; /* Blue */
  font-size: 36px;
}

p {
  color: #666;
  font-size: 18px;
}
```

#### 6. Configure Nginx
* Open the default Nginx configuration file for editing:
```bash
sudo nano /etc/nginx/sites-available/default
```
* Replace the default content with the following configuration:
```
server {
  listen 80;
  server_name your_domain_name; # Replace with your domain name or server IP

  root /home/ubuntu/mywebsite;
  index index.html index.htm;

  location / {
    try_files $uri $uri/ /index.html;
  }
}
```

#### 7. Test Nginx Configuration and Restart
* Check for configuration errors:
```bash
sudo nginx -t
```
* Restart Nginx:
```bash
sudo systemctl restart nginx
```

#### 8. Access Your Website
* Open a web browser and enter your EC2 instance's public IP address or your domain name (if configured). You should see your website.

### Additional Notes
* Consider security measures like firewalls, SSH key-based authentication, and regular security updates.
* Explore performance optimization techniques like image compression, CDNs (Content Delivery Networks), and caching strategies.
* Investigate scaling options for increased website traffic (e.g., using load balancers).
* Implement website monitoring tools to track performance and resource usage.

This guide serves as a basic starting point. You can customize it further by adding more website content, exploring advanced Nginx configurations, and implementing security best practices.
 
**Note:** Remember to replace `your_domain_name` with your actual domain name or server IP. Also, ensure that the web server user (usually `www-data`) has appropriate permissions to access the `/home/ubuntu/mywebsite` directory and its contents.
 
**Would you like to learn more about setting permissions for the web server user?**
