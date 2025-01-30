# Static Site Server Setup

## Overview
This project demonstrates how to set up a basic Linux server and configure it to serve a static site using Nginx. It also covers using `rsync` to deploy your changes to the server.

## Requirements
- Register and set up a remote Linux server on any provider (e.g., DigitalOcean, AWS).
- Ensure SSH access to your server.
- Install and configure Nginx to serve a static site.
- Create a simple webpage with basic HTML, CSS, and image files.
- Use `rsync` to update the remote server with the local static site.
- Optionally, point a domain name to your server and serve the static site from there.

## Steps

### 1. Register and Set Up a Remote Linux Server
Register and set up a droplet on **DigitalOcean** (or any other provider). Connect to your server using SSH:

```bash
ssh root@your-droplet-ip
```

### 2. Install and Configure Nginx
#### Update your server:
```bash
sudo apt update
sudo apt upgrade -y
```

#### Install Nginx:
```bash
sudo apt install nginx -y
```

#### Start and enable Nginx:
```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

#### Verify Nginx is running:
Open a web browser and navigate to `http://your-droplet-ip`. You should see the Nginx welcome page.

### 3. Create a Simple Webpage
#### Navigate to the web root directory:
```bash
cd /var/www/html
```

#### Create a new `index.html` file:
```bash
sudo nano index.html
```

#### Add basic HTML content:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Static Site</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Welcome to My Static Site</h1>
    <img src="image.jpg" alt="Sample Image">
    <p>This is a basic static site served using Nginx.</p>
</body>
</html>
```

#### Create a CSS file:
```bash
sudo nano styles.css
```

#### Add basic CSS content:
```css
body {
    font-family: Arial, sans-serif;
    text-align: center;
}
h1 {
    color: #333;
}
```

#### Upload an image to the web root directory (e.g., `image.jpg`).

### 4. Use `rsync` to Deploy Changes
#### Install `rsync` on your local machine (if not already installed):
```bash
brew install rsync
```

#### Create a `deploy.sh` script:
```bash
nano deploy.sh
```

#### Add the following content to `deploy.sh` (replace `your-droplet-ip` with your actual IP address):
```bash
#!/bin/bash
rsync -avz --delete -e ssh ./ root@your-droplet-ip:/var/www/html/
```

#### Make the script executable:
```bash
chmod +x deploy.sh
```

#### Run the script to deploy your site:
```bash
./deploy.sh
```
https://roadmap.sh/projects/static-site-server
### 5. Point Domain Name to Your Server (Optional)
- Update your **DNS settings** to point to your server's IP address.
- Update **Nginx configuration** to use your domain name (if needed).

  
