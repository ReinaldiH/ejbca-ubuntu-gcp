# Installing EJBCA Community on Ubuntu Server 22.04 LTS with Docker (GCP Instance Setup)

## Introduction
In this guide, I will install EJBCA Community using Ubuntu Server 22.04 LTS. You are free to use any Linux OS that you find more comfortable. Here, I am using Google Cloud Platform as the server.

## 1. Creating an Instance in GCP
To get started, open your GCP account, create a new instance, select the OS, and configure the specifications according to your needs.

![Create instance](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*jrRkUo1KKS6VhxngLYIsFA.png)


## 2. Update and Upgrade OS
First, update and upgrade your OS to ensure that all modules and packages are up to date.
```bash
sudo apt update && sudo apt upgrade -y
```
If you are using a local server, enter the server password as needed.

## 3. Install Docker
Next, we will install Docker from the official repository. Follow these steps:

1. Install prerequisite packages:
```bash
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
```

2. Add the Docker GPG key:
```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

3. Add the Docker repository:
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

4. Update package lists again:
```bash
sudo apt update
```

5. Install Docker:
```bash
sudo apt install docker-ce -y
```

6. Ensure Docker is running:
```bash
sudo systemctl status docker
```

## 4. Pull EJBCA Image from Docker Hub
```bash
sudo docker pull keyfactor/ejbca-ce
```

## 5. Running the EJBCA Container
```bash
docker run -it --rm -p 80:8080 -p 443:8443 -h localhost -e TLS_SETUP_ENABLED="true" keyfactor/ejbca-ce
```

Wait until the process completes and the terminal displays success logs.

## 6. Accessing the EJBCA Web UI
Once the container is running, copy the URL displayed in the terminal and open it in a browser (Mozilla recommended).
If a security warning appears:
1. Click **Advanced**
2. Select **Accept the Risk and Continue**

## 7. Superadmin Login
Enter the password displayed in the terminal logs as the Enrollment Code.

1. Select **Key Algorithm** → **2048 bits**
2. Click **Download PKCS#12**

## 8. Importing the Certificate into the Browser
On Mozilla Firefox:
1. **Settings** → **Privacy & Security**
2. **View Certificates** → **Import**
3. Select the downloaded **.p12** file
4. Enter the password

## 9. Accessing the EJBCA Web UI
After importing the certificate, reopen **localhost**, and the EJBCA Web UI should appear.

If a security warning appears:
1. Click **Advanced**
2. Select **Accept the Risk and Continue**

## 10. Installation Successful 🎉
If everything is set up correctly, the EJBCA Web UI will appear as shown in the following image.

Congratulations! You have successfully installed EJBCA Community on Ubuntu Server 22.04 LTS using Docker!
