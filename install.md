- Go to OVH website at https://www.ovhcloud.com/en-ca/vps/

- Buy a VPS by following the steps on the website

- Use the credentials received by email to login:
	* ssh IP address

- Change admin password for security reasons:
	* passwd 
	Enter current password when prompted, followed by new one

- Create regular users and add them to sudo group:
	* sudo adduser newuser
	* usermod -aG sudo newuser

- Update system with latest stable packages:
	* apt-get update
	* apt-get upgrade

- Create a private-public SSH key for each of the users (this is to login in without requiring a password:
	* mkdir ~/.ssh
	The command will prompt you to save the key, do not change the directory
	* ssh-keygen -b 4096
	Get your public key and copy it
	* cat ~/.ssh/id_rsa.pub
	
- Add SSH keys to the created server
	Login to server
	* ssh newuser@ipaddress
	Enter password
	Create .ssh file
	* mdkir ~/.ssh
	* vim ~/.ssh/authorized_keys 
	Paste the public key copied earlier
	Save the changes
	* :wq
	* systemctl restart sshd
	You can now login user "newuser@ipaddress" without entering a password

- Update packages of the server:
	* sudo apt-get update 

- Install nginx package:
	* sudo apt-get install nginx

- Check service status:
	* systemctl nginx.service
	nginx should already be running

- Server is now working (can type IP or domain name in browser)

- Create a file for each team member:
	* cd /var/www/html
	* mkdir teamMemberName
	Bring all files and websites to be added and put them inside created folder

- The website can now be accessed through entering the following link in a web sbrowser
	http://vps-ip/teamMemberName

- Install Ruby and Jekyll:
	* sudo apt-get install ruby-full build-essential zlib1g-dev
	* echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
	* echo 'export GEM_HOME="$HOME/gems" >> ~/.bashrc
	* source ~/.bashrc
	* sudo gem install jekyll bundler

- Create a website:
	* jekyll new websiteName
	* cd wesiteName
	* bundle exec jekyll serve

- The website can now be accessed through entering the following link in a web browser:
	http://localhost:4000

- Change website theme (optional)
	Open Gemfile
	* vim Gemfile
	Add theme
	* gem "jekyll-theme-nameOfTheme"
	Save changes
	* :wq
	Install the theme
	* bundle install
	Open _config.yml file
	* vim _config.yml
	Change line starting with "theme: " to "theme: jekyll-theme-nameOfTheme"
	Save changes
	* :wq
 
- Create .gitignore file and add _site to it:
	* vim .gitignore
	Add the lines: 
	_site
	.jekyll-metadata
	*-cache/

	Save changes
	* :wq

- Log onto vps:
	* ssh newuser@vps-ip

- Install Ruby and Jekyll in server following same steps as before:
	* sudo apt-get install ruby-full build-essential zlib1g-dev
	* echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
	* echo 'export GEM_HOME="$HOME/gems" >> ~/.bashrc
	* source ~/.bashrc
	* sudo gem install jekyll bundler

- Get the website created earlier (can be done through github)

- Build website using nginx:
	* sudo bundle exec jekyll build

- Copy content of _site/ to /var/www/html/
	* sudo cp -a _site/. /var/www/html/

- The website is now working (can type vps-ip in browser's URL)

- Convert all HTML pages of website to .md files:
	* sudo cp pageName.html pageName.md

- Include layout for page:
	* vim pageName.md
	At the very top, add lines:
	---
	layout: default
	---

	Save changes
	* :wq

- Send the .md file(s) and all other data that the website requires (images, videos, etc.) to the websiteName folder 
	* sudo cp pageName.md /home/teamWebsite/
	Do the same for all other files

- Modify _config.yml and index.markdown files if any changes to the header of the website are desired to be made

- Build the site:
	* sudo bundle exec jekyll build
	* sudo cp -a _site/. /var/www/html

