Flask Static Site Deployment on AWS EC2

Project Name:
Flask Static Website Deployment on Amazon Linux EC2

Objective:
To deploy a Python Flask-based static website on an Amazon EC2 instance running Amazon Linux, making it publicly
accessible via EC2's public IP and custom port 8000.

Prerequisites:
- AWS Account
- Flask application code (on GitHub)
- EC2 instance (Amazon Linux)
- Security Group access to custom ports (8000)
Step-by-Step Deployment Guide

1. Launch EC2 Instance
- AMI: Amazon Linux 2
- Instance Type: t2.micro (Free Tier eligible)
- Key Pair: Create or use existing
- Security Group: Allow port 22 (SSH) and 8000 (Custom TCP)

2. Connect to EC2 via SSH
ssh -i your-key.pem ec2-user@<EC2-public-IP>

3. Install Required Packages
sudo yum update -y
sudo yum install python3 git -y

4. Clone Your Flask Project from GitHub
git clone https://github.com/your-username/your-repo.git
cd your-repo

5. Set Up Python Virtual Environment
python3 -m venv venv
source venv/bin/activate

6. Install Flask and Other Dependencies
pip install -r requirements.txt

7. Run the Flask Application
Ensure site.py contains:
app.run(host='0.0.0.0', port=8000)
Then run:
python3 site.py

8. Update EC2 Security Group (if not already done)
Allow Custom TCP:
- Port: 8000
- Source: 0.0.0.0/0

9. Access the App in Browser
http://<EC2-public-IP>:8000
Outcome:
Your Flask static site is now live and accessible from anywhere via the EC2 public IP and port 8000.
Important Notes:
- The built-in Flask server is for development only. For production use, consider setting up Gunicorn + Nginx.
- Avoid exposing your instance with open ports in a real-world production app without proper firewall and security settings.
Next Steps:
- Add Gunicorn as a WSGI server for better performance
- Configure Nginx as a reverse proxy
- Use a domain name and SSL for production
