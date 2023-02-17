
# Jenkins

## Installation
```sh
# Install Java
sudo apt update
sudo apt install openjdk-11-jre
# Install jenkins
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins
# Enable jenkins service to start at boot
sudo systemctl enable jenkins
```
> * To open the jenkins port in ubuntu
```sh
sudo ufw allow 8080
```
## References: 
* https://www.jenkins.io/doc/book/installing/linux/#debianubuntu