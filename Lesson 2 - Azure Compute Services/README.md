## Create a Linux Virtual Machine

**Prerequisite**: If you're using Windows, you’ll need PowerShell or Bash to connect to the VM with ssh. Windows 10 should already have Powershell installed. If you don't have it already installed, here is a [guide](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell-core-on-windows?view=powershell-7&WT.mc_id=udacity_learn-wwls) on how to install it.

1. Create a Linux VM called “linux-vm-west” inside “resource-group-west”. The VM should have the following configurations:

* VM Name: "linux-vm-west"
* Region: West US or the closest region to you that's available
* Availability Options: No infrastructure redundancy required.
* Image: Ubuntu Server (any version)
* Azure Spot instance: No
* Size: Standard B1ls
* Authentication type: Password
* Username: (any username you choose)
* Password: (any password you choose)
* Inbound Port Rules: Allow both 22 and 80

2. After creating the VM, use **secure copy** to copy the `web` directory from [here](https://video.udacity-data.com/topher/2020/July/5f1875e2_create-vm-starter/create-vm-starter.zip) to the VM. 
`scp -r ./web <USERNAME>@<IPADDRESS>:/home/<USERNAME>`

3. After copying the files to the VM, **connect** to it and run the command `ls` to check the `web` directory is on the VM.

4. Next, install `python3-env` and `nginx` 

`sudo apt-get -y update && sudo apt-get -y install nginx python3-venv`

5. Next, configure nginx to listen for incoming traffic on port 80 and set port 3000 as the proxy.

* Navigate to `/etc/nginx/sites-avaiable`
* Remove the `default` file
* Replace it with a file containing:

```
server {
  listen 80;
  location / {
      proxy_pass http://localhost:3000;
      proxy_http_version 1.1;
      proxy_set_header Upgrade $http_upgrade;
      proxy_set_header Connection keep-alive;
      proxy_set_header Host $host;
      proxy_cache_bypass $http_upgrade;
  }
}
```

* After saving the file, restart nginx `sudo service nginx restart`

6. Change to the `web` directory and create and activate a virtual env
7. As a best practice, update pip in a newly created virtual env
8. Install dependencies from **requirements.txt**
9. Run the application and visit the public IP address in your browser. You should see the application running if done correctly.

#### Cleanup

Once you're done with the exercise, be sure to delete the VM and it's resources to avoid incurring unwanted charges.

**Note:** Azure free accounts only allow 750 hours of free hosting. Make sure to delete this VM after completing the exercise to avoid charges.

Supporting Materials
 [create-vm-starter.zip](https://video.udacity-data.com/topher/2020/July/5f1875e2_create-vm-starter/create-vm-starter.zip)
