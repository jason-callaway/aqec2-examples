# aqec2-examples
Example playbooks for the aqec2 Ansible Galaxy role

## Setup

Install the Ansible Galaxy role, and download the EC2 dynamic inventory scripts.

```
mkdir -p ansible/roles
mkdir -p ansible/inventory/aws
ansible-galaxy install -p ansible/roles jason-callaway.aqec2
curl https://raw.githubusercontent.com/ansible/ansible/v2.3.1.0-1/contrib/inventory/ec2.ini -o ansible/inventory/aws/ec2.ini
curl https://raw.githubusercontent.com/ansible/ansible/v2.3.1.0-1/contrib/inventory/ec2.py -o ansible/inventory/aws/ec2.py
chmod 755 ansible/inventory/aws/ec2.py
```

Build the aqec2 OCI image.

```
docker build -t aqec2 -f roles/jason-callaway.aqec2/files/Dockerfile .
```

Copy your access key to this repo's directory. Be sure to name it ```aqec2.pem```, which is already in ```.gitignore```, or add your key name to ```.gitignore```. Also copy your relevant AWS config and credentials files. Same deal with them, if you use the standard names, they're already in ```.gitignore```.

```
cp path/to/key.pem ./a2ec2.pem
cp ~/.aws/config ./aws_config
cp ~/.aws/credentials ./aws_credentials
```

Now you can run your playbook from the OCI image with the ```run.sh``` script.

```
cp site.yml ansible/
run.sh site.yml
```
