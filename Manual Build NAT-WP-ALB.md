
1. VPC
    - Name:
    - IPv4 CIDR: 10.0.0.0/16
2. IGW
    - Name
3. Attach IGW
4. Subnets
    - Public Subnet 1
        - Select VPC
        - Name
        - AZ Main
        - IPv4 CIDR: 10.0.1.0/24
    - Public Subnet 2
        - Name
        - AZ Backup
        - IPv4 CIDR: 10.0.2.0/24
    - Private Subnet 1
        - Name
        - AZ Main
        - IPv4 CIDR: 10.0.3.0/24
5. Elastic IP
6. Route Tables Part 1
    - Public 1 Route Table
        - Name
        - VPC
        - Destination: 10.0.0.0/16 Target: Local
        - Destination: 0.0.0.0/0 Target: IGW (ID of IGW)
        - Subnet Association
            - Public Subnet 1
    - Public 2 Route Table
        - Name
        - VPC
        - Destination: 10.0.0.0/16 Target: Local
        - Destination: 0.0.0.0/0 Target: IGW (ID of IGW)
        - Subnet Association
            - Public Subnet 2
    - Private 1 Route Table
        - Name
        - VPC
        - Destination: 10.0.0.0/16 Target: Local
        - Subnet Association
            - Private Subnet 1
7. Security Groups Part 1
    - NAT EC2 Security Group
        - Name
        - Description
        - VPC
        - Inbound
            - Rule 1
                - Type: All ICMP - IPv4
                - Source: Custom - CIDR of Private Subnet
            - Rule 2
                - Type: All Traffic
                - Source: Custom - CIDR of Private Subnet
            - Rule 3
                - Type: SSH
                - Source: [Custom - 0.0.0.0/0] or [My IP]
        - Outbound
            - Rule 1
                - Type: All Traffic
                - Source: Custom - 0.0.0.0/0
    - ALB Security Group
        - Name
        - Description
        - VPC
        - Inbound
            - Rule 1
                - Type: HTTP
                - Source: Custom - 0.0.0.0/0
            - Rule 2
                - Type: HTTPS
                - Source: Custom - 0.0.0.0/0
        - Outbound
    - Wordpress Ubuntu EC2 Security Group
        - Name
        - Description
        - VPC
        - Inbound
            - Rule 1
                - Type: SSH
                - Source: Custom - NAT Instace Security Group ID
            - Rule 2
                - Type: HTTP
                - Source: Custom - ALB Security Group ID
            - Rule 3
                - Type: HTTPS
                - Source: Custom - ALB Security Group ID
        - Outbound
            - Rule 1
                - Type: All Traffic
                - Source: Custom - NAT Instace Security Group ID
            - Rule 2
                - Type: MYSQL/Aurora
                - Source: Custom - 127.0.0.1/32
8. Security Groups Part 2
    - NAT EC2 Security Group
        - Outbound
            - Rule 2
                - Type: SSH
                - Source: Custom - Security Group ID of WordPress Ubuntu Instance
    - ALB Security Group
        - Outbound
            - Rule 1
                - Type: All Traffic
                - Source: Custom - Security Group ID of WordPress Ubuntu Instance
9. ***TERRAFORM SCRIPT***
Create Key Pair
    - Name
    - RSA
    - .pem
    *** NOTE: Key will automatically download to laptop
    *** NOTE: This is done on my Ubuntu laptop I am using.
10. ***TERRAFORM SCRIPT*** 
Configure Key Pair 
    - cd Downloads
    - chmod 400 [.pem file name]
    *** NOTE: This is done on my Ubuntu laptop I am using.
11. ***TERRAFORM SCRIPT*** 
Launch NAT EC2 Instance
    - Name
    - OS
        - Amazon Linux 2023 AMI
        - t2.micro
    - Key Pair
    - Network Settings
        - VPC 
        - Subnet: Public 1 Subnet
        - Auto Assign Public IP: Enabled
    - NAT EC2 Security Group
12. ***TERRAFORM SCRIPT***
Associate Elastic IP to NAT 
    - Select EIP
    - Allocate EIP
    - Instance
        - NAT EC2 Instance
        - Check box Allow this Elastic IP address to be reassociated
13. ***SSM AGENT*** 
Configure NAT EC2 Instance in Terminal
    - ssh -i ~/Downloads/[key file name] ec2-user@[EIP]
    - sudo vi /etc/sysctl.d/custom-ip-forwarding.conf
        - Paste in file: net.ipv4.ip_forward=1
        - :wq!
    - sudo sysctl -p /etc/sysctl.d/custom-ip-forwarding.conf
    - sudo yum install iptables-services -y
    - netstat -i
        - NOTE: First Interface is needed for the following command
    - sudo iptables -t nat -A POSTROUTING -o enX0 -j MASQUERADE
    - sudo iptables -A FORWARD -i eth0 -o enX0 -m state --state RELATED,ESTABLISHED -j ACCEPT
    - sudo iptables -A FORWARD -i eth0 -o enX0 -j ACCEPT
    - sudo service iptables save
    - sudo service iptables restart
14. ***TERRAFORM SCRIPT*** 
Configure NAT EC2 Instance in AWS Console
    - Select NAT Instnace
    - Actions Button
        - Networking
            - Change Source/Destination Check
                - Check Box: Stop
15. ***TERRAFORM SCRIPT***
Route Tables Part 2
    - Private Route Table
        - Destination: 0.0.0.0/0 Target: Instance (NAT EC2 Instance) ***This will change automatically to Network Interface eni of NAT
16. ***TERRAFORM SCRIPT***
Launch WordPress Ubuntu EC2 Server
    - Name
    - OS
        - Ubuntu Server 24.04 LTS (HVM)
        - t2.micro
    - Key Pair
    - Network Settings
        - VPC
        - Private Subnet 1
        - Auto-assign Public IP - Disabled
    - WordPress Ubuntu EC2 Security Group 
17. ***SSM AGENT*** 
Configure WordPress Ubuntu EC2 after Launch
    - In terminal on local laptop
        - ssh-add /path/to/.pem/file
    - ssh -A -i ~/path/to/.pem/file ec2-user@[NAT PUBLIC IP]
    - ssh ubuntu@[Private IP Address]
    - sudo apt update
    - sudo apt install nginx
    - sudo apt install mysql-server
    - sudo mysql
    - EXIT;
    - sudo apt install php-fpm php-mysql php-curl php-gd php-mbstring php-xml php-xmlrpc php-zip
    - php --version
    - sudo mkdir /var/www/demo
    - sudo chown -R $USER:$USER /var/www/demo
    - sudo vi /etc/nginx/sites-available/demo
        - Copy into vi file
                server {
                listen 80;
                server_name your_IPv4;
                root /var/www/demo;

                index index.html index.htm index.php;

                location / {
                try_files $uri $uri/ /index.php?$args;
                }

                location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/var/run/php/php8.3-fpm.sock;
                }

                location ~ /\.ht {
                deny all;
                }
                }
        - ctrl+shift+v to copy
        - :wq!
    - sudo ln -s /etc/nginx/sites-available/demo /etc/nginx/sites-enabled/
    - sudo unlink /etc/nginx/sites-enabled/default
    - sudo nginx -t
    - sudo systemctl reload nginx
    - sudo mysql
    - CREATE DATABASE demo DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
    - CREATE USER 'demo_user'@'localhost' IDENTIFIED BY 'demo123';
    - GRANT ALL ON demo.* TO 'demo_user'@'localhost';
    - EXIT;
    - cd /tmp
    - curl -LO https://wordpress.org/latest.tar.gz
    - sudo tar -xzvf latest.tar.gz
    - sudo cp /tmp/wordpress/wp-config-sample.php /tmp/wordpress/wp-config.php
    - sudo cp -a /tmp/wordpress/. /var/www/demo
    - sudo chown -R www-data:www-data /var/www/demo
    - sudo vi /var/www/demo/wp-config.php
        - Remove default DB_NAME, DB_USER, and DB_Password
        - Replace defaults with
            - DB_NAME 'demo'
            - DB_USER 'demo_user'
            - DB_PASSWORD 'demo123'
        - :wq!
    - curl -s https://api.wordpress.org/secret-key/1.1/salt/
        - copy security keys
            define('AUTH_KEY', 'O 5ve+ZTt]:xk|7|KLAG&AmM+C5k3Y)0eN$I+|3l|oLM}{(%V<;.)Y6@LNh*9zF.');
            define('SECURE_AUTH_KEY','.&DVo|RwZCz:jd@:72uTgk|`Sl /zKK>F%l1OSDZW1ZoA<Q(E-;?^(^EZc>$vt/5');
            define('LOGGED_IN_KEY','[MT)ghG^DS-s7WufQ}UeF*x=<=|TU>IB>vr~8=>V4td[3*V5d.jNyPE}Iv`jX0m1');
            define('NONCE_KEY','/-a_A>c|O9~Ywt&%=B1$z6$?aQeYyi8(/$TGP<N>QCv=<a@&y@WfX1Ky>G~3A]wU');
            define('AUTH_SALT','P`LW9-4,Fu6cbG67;||h*W9hYEMgZKJeL|/I~o$o87BWLNqfE~%VHqNa[YF1G#I0');
            define('SECURE_AUTH_SALT','wk4vlZ6r~X(/ RT1U^ Fz/A&@*Upm &FrL/e HC^K_7yd m>Cab ,ps?y/r~Lt~P');
            define('LOGGED_IN_SALT','n1b}&N+.)u6me0nmW`$vWP#orAD6xj?)FsW<I99B)5ll<KR>N0cJq5f5Y[97kIou');
            define('NONCE_SALT','@JstL?5e:$TbM/hTXhPv/WE]:`:m/[5?Pup]79-_8w=5+3+-@j7GP?E=IU6i-!^8');
        - paste in sudo vi /var/www/demo/wp-config.php
        - Replace the following: define( 'AUTH_KEY',         'put your unique phrase here' );
            - define( 'SECURE_AUTH_KEY',  'put your unique phrase here' );
            - define( 'LOGGED_IN_KEY',    'put your unique phrase here' );
            - define( 'NONCE_KEY',        'put your unique phrase here' );
            - define( 'AUTH_SALT',        'put your unique phrase here' );
            - define( 'SECURE_AUTH_SALT', 'put your unique phrase here' );
            - define( 'LOGGED_IN_SALT',   'put your unique phrase here' );
            - define( 'NONCE_SALT',       'put your unique phrase here' );
    - sudo systemctl restart php8.3-fpm
18. ***TERRAFORM SCRIPT***
Create Target Group for Application Load Balancer
    - In EC2 Dashboard
    - Select Target Group
    - Click Create Target Group Button
        - Instances
        - Name
        - IPv4
        - Select VPC
        - HTTP1
        - Path:  /var/www/demo/index.php
        - Next
        - Select WordPress Sever
        - Create Target Group
19. ***TERRAFORM SCRIPT***
Register targets to Target Group
    - EC2 Dashboard
    - Select Target Groups
    - Select Target Group created above
    - Select Targets Tab
    - Click Register Targets Button
    - Select Wordpress Instance
    - Click Include as Pending Below Button
    - Click Register Pending Targets
20. ***TERRAFORM SCRIPT***
Configure Application Load Balancer
    - In EC2 Dashboard
    - Select Load Balancer
    - Click Create Load Balancer
    - Under Application Load Balancer click Create Button
        - Name
        - Internet-Facing
        - IPv4
        - Select VPC
        - Select both Availability Zones that are the Public Subnets
        - Remove Default Secuirty Group
        - Select ALB Security Group
        - Select Target Group
        - Click Create Load Balancer
21. ***SSM AGENT*** 
Update /etc/nginx/sites-available/demo with ALB DNS name
    - In Terminal on local laptop
        - ssh-add /path/to/.pem/file
        - ssh -A -i ~/path/to/.pem/file ec2-user@[NAT PUBLIC IP]
        - ssh ubuntu@[Private IP Address]
        - sudo vi /etc/nginx/sites-available/demo
        - Replace your_IPv4 with ALB DNS name
        - :wq!








