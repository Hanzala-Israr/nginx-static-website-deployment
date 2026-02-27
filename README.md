# Static Website Deployment on Nginx (EC2 Ubuntu)

This project demonstrates how to deploy a static website using **Nginx** on an **AWS EC2 Ubuntu instance**.
The website is served over HTTP using a configured Nginx server block.

This project is part of a DevOps learning journey and covers server setup, web server configuration, and deployment.

---

## Technologies Used

- AWS EC2 (Ubuntu)
- Nginx
- Linux
- HTML/CSS/JS
- SSH

---

## Step 1: Launch EC2 Instance

1. Go to AWS Console
2. Launch an EC2 instance
3. Choose:
   - Ubuntu
   - t2.micro (Free tier eligible)
4. Allow inbound traffic:
   - SSH (Port 22)
   - HTTP (Port 80)
5. Download the key pair

---

## Step 2: Connect to EC2

```bash
ssh -i your-key.pem ubuntu@your-ec2-public-ip
```

Example:

```bash
ssh -i mykey.pem ubuntu@16.170.159.226
```

---

## Step 3: Update Packages

```bash
sudo apt update
sudo apt upgrade -y
```

---

## Step 4: Install Nginx

```bash
sudo apt install nginx -y
```

Start Nginx:

```bash
sudo systemctl start nginx
```

Enable Nginx:

```bash
sudo systemctl enable nginx
```

Check status:

```bash
sudo systemctl status nginx
```

---

## Step 5: Create Website Directory

```bash
sudo mkdir -p /var/www/static-site
```

---

## Step 6: Add Website Files

Copy your static website files:

```bash
sudo cp -r * /var/www/static-site/
```

Or create a test file:

```bash
echo "Hello from Nginx" | sudo tee /var/www/static-site/index.html
```

---

## Step 7: Configure Nginx

Create a new configuration file:

```bash
sudo nano /etc/nginx/sites-available/static-site
```

Add the following configuration:

```nginx
server {
    listen 80;
    server_name _;

    root /var/www/static-site;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

---

## Step 8: Enable the Site

```bash
sudo ln -s /etc/nginx/sites-available/static-site /etc/nginx/sites-enabled/
```

---

## Step 9: Disable Default Site

```bash
sudo rm /etc/nginx/sites-enabled/default
```

---

## Step 10: Test Configuration

```bash
sudo nginx -t
```

Expected output:

```
syntax is ok
test is successful
```

---

## Step 11: Restart Nginx

```bash
sudo systemctl restart nginx
```

---

## Step 12: Access Website

Open in browser:

```
http://your-ec2-public-ip
```

Example:

```
http://16.170.159.226
```

---

## Author

Hanzala Israr
