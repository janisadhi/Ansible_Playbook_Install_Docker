
# Ansible Playbook to Install Docker on Production Server

This repository contains an Ansible playbook designed to automate the installation of Docker on a production server running Ubuntu. The playbook installs Docker, Docker Compose, and other prerequisites needed for setting up a Docker environment on your server.

## Prerequisites

1. **Ansible**: Ensure you have Ansible installed on your local machine. If not, install it by following the [official documentation](https://docs.ansible.com/ansible/latest/installation_guide/).
   
2. **Access to a production server**: You must have SSH access to the production server where Docker will be installed.

3. **Public SSH key**: Your public  SSH key should be added to the `authorized_keys` file on the production server.

## Steps to Set Up and Run the Playbook

1. **Clone the repository**:
   ```bash
   git clone https://github.com/janisadhi/Ansible_Playbook_Install_Docker.git
   cd Ansible_Playbook_Install_Docker
   ```

2. **Configure the `hosts` file**:
   In the `hosts` file, update it with your production server’s IP address and SSH username:
   ```ini
   [production]
   <your-server-ip> ansible_user=<your-server-username>
   ```

3. **Add your SSH public key to the production server**:
   Make sure your public SSH key is added to the `authorized_keys` on the server for authentication.

4. **Check the connection**:
   To verify that Ansible can connect to your server, run the following command:
   ```bash
   ansible -i hosts production -m ping
   ```

5. **Run the playbook**:
   Use the following command to execute the playbook and install Docker on the server:
   ```bash
   ansible-playbook -i hosts playbook-docker.yml -l production
   ```

6. **Verify the Docker installation**:
   After the playbook has completed, you can verify Docker’s installation by running:
   ```bash
   ansible -i hosts production -a "docker -v"
   ```

## Playbook Explanation

The playbook performs the following tasks:

1. **Update apt cache**: It updates the apt cache to ensure that we have the latest package information.
2. **Install prerequisites**: Installs required packages like `ca-certificates`, `curl`, and `gnupg`.
3. **Create apt keyring directory**: Sets up the keyring directory to store Docker's GPG key.
4. **Add Docker's official GPG key**: Downloads and stores Docker’s official GPG key to authenticate the Docker packages.
5. **Add Docker apt repository**: Adds the official Docker apt repository to the server's sources list.
6. **Update apt cache again**: Refreshes the apt cache after adding the Docker repository.
7. **Install Docker packages**: Installs Docker and the necessary components like `docker-ce`, `docker-ce-cli`, `containerd.io`, `docker-compose-plugin`, and `docker-buildx-plugin`.


## Author

Janis Adhikari

```

This README provides clear instructions for setting up and running the playbook, including prerequisites, setup steps, and verification of Docker installation.