# Online Shopping Cart (E-Commerce Website)

📌 Project Overview
An end-to-end CI/CD pipeline implementation for a Java-based Online Shopping Cart web application. The project demonstrates automated Build & Deployment using Jenkins, Maven, and Apache Tomcat on an AWS EC2 instance.
Whenever source code is pushed to the GitHub repository, Jenkins automatically pulls the latest code, builds and packages it using Maven, and deploys the generated WAR file to the Tomcat web server — with zero manual intervention.

🏗️ Architecture
Developer → GitHub Repo → Jenkins (Port 8080)
                               ↓
                         Maven Build
                               ↓
                         WAR File Generated
                               ↓
                    Tomcat Server (Port 9090)
                               ↓
                    Application Live on Browser

⚙️ Tech Stack
LayerTechnologyApplicationJava, JDBC, Servlets, JSPFrontendHTML, CSS, JavaScript, BootstrapDatabaseMySQLBuild ToolApache MavenCI/CDJenkinsWeb ServerApache Tomcat 9CloudAWS EC2 (Amazon Linux)Version ControlGit & GitHub

🚀 CI/CD Pipeline Flow

Developer pushes code changes to GitHub
Jenkins detects the change via webhook or polling
Jenkins pulls the latest code from the GitHub repository
Maven compiles and packages the code into a .war file
Jenkins deploys the WAR file to Apache Tomcat using the Deploy to Container plugin
Application is accessible live on the browser


🖥️ Infrastructure Setup
AWS EC2 Instance

OS: Amazon Linux 2
Jenkins running on Port 8080
Tomcat running on Port 9090
Security Group inbound rules: 8080, 9090 open

Jenkins Installation
bashsudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo amazon-linux-extras install java-openjdk11 -y
sudo yum install jenkins -y
sudo systemctl enable jenkins
sudo systemctl start jenkins
Tomcat Installation
bashsudo wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.73/bin/apache-tomcat-9.0.73.tar.gz
tar -xvf apache-tomcat-9.0.73.tar.gz
cd apache-tomcat-9.0.73/bin
./startup.sh
Tomcat Port Changed to 9090

Edited conf/server.xml → Changed Connector port from 8080 to 9090

Tomcat Users Configured (conf/tomcat-users.xml)
xml<role rolename="manager-gui" />
<role rolename="manager-script" />
<role rolename="admin-gui" />
<user username="tomcat" password="tomcat" roles="manager-gui" />
<user username="admin" password="admin" roles="manager-gui,admin-gui,manager-script" />

🔧 Jenkins Configuration
Plugins Installed

Deploy to Container — for automated WAR deployment to Tomcat
Git Plugin — for GitHub integration
Maven Integration — for build management

Jenkins Job Setup

Source: GitHub repository URL
Build trigger: Build periodically
Build: clean install (Maven goals)
Post-build: Deploy WAR to Tomcat container using manager-script credentials
<img width="1366" height="730" alt="image" src="https://github.com/user-attachments/assets/050e3cf8-6570-4877-8bf1-f042c106c46f" />


🗄️ Database Setup
bash# Login to MySQL
mysql -u root -p

# Run the SQL script
source databases/mysql_query.sql
Update database credentials in src/main/resources/application.properties:
propertiesdb.username=your_mysql_username
db.password=your_mysql_password
mailer.email=your@gmail.com
mailer.password=your_gmail_app_password

🌐 Access the Application
ServiceURLJenkins Dashboard http://<EC2-Public-IP>:8080
Application http://<EC2-Public-IP>:9090/shopping-cart/
Tomcat Manager http://<EC2-Public-IP>:9090/manager
<img width="1366" height="728" alt="image" src="https://github.com/user-attachments/assets/f84e79b8-445a-45f1-ab29-623da389ee3f" />


📁 Project Structure
shopping-cart/
├── src/
│   └── main/
│       ├── java/          # Servlets, JDBC, business logic
│       └── resources/     # application.properties
├── WebContent/            # JSP pages, HTML, CSS, JS
├── databases/
│   └── mysql_query.sql    # Database initialization script
├── conf/                  # Tomcat configuration files
├── pom.xml                # Maven build configuration
└── README.md

👨‍💻 Author
Sandip Kumar Ray
