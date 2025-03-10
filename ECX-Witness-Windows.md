# Quick Start Guide (QSG) for Setting Up a Witness Server in EXPRESSCLUSTER Environment

## Prerequisites
Before proceeding, ensure that the witness server meets the system requirements specified in the official documentation:  
[System Requirements for the Witness Server](https://docs.nec.co.jp/software/clustering/expresscluster_x/x52/ecx_x52_windows_en/W52_SG_EN/W_SG.html#system-requirements-for-the-witness-server)

## Step 1: Install Node.js on the Witness Server 
1. Download and install Node.js (18.13.0 or 20.10.0) from the official website:
   - [Node.js Download](https://nodejs.org/en/download)


## Step 2: Install the Required NPM Package
1. Obtain the Witness server package (`clpwitnessd-<version>.tgz`) from the EXPRESSCLUSTER DVD-ROM:
   ```
   Common\<version>\common\tools\witnessd\clpwitnessd-<version>.tgz
   ```
2. Install the Witness server service globally using:
   ```sh
   npm install --global clpwitnessd-<version>.tgz
   ```

## Step 3: Configuration
1. Find the installation directory:
   ```sh
   npm list --global clpwitnessd
   ```
   Example output:
   ```
   C:\Users\Administrator\AppData\Roaming\npm
   `-- clpwitnessd@5.2.0
   ```
2. Navigate to the installation folder and edit `clpwitnessd.conf.js`:
   ```
   C:\Users\Administrator\AppData\Roaming\npm\node_modules\clpwitnessd\clpwitnessd.conf.js
   ```
3. Update the configuration settings as needed:
   - Enable/disable HTTP/HTTPS
   - Set port numbers
   - Define log levels and locations

## Step 4: Start Witness Server
### Run in Foreground Mode
```sh
clpwitnessd
```

### Register as an OS Service
#### Windows
1. Install `winser`:
   ```sh
   npm install --global winser
   ```
2. Create a folder for execution logs, SSL keys, etc.
3. Create `package.json` in that folder:
   ```json
   {
     "name": "clpwitnessd-service",
     "version": "5.2.0",
     "license": "UNLICENSED",
     "private": true,
     "scripts": {
       "start": "C:\\Users\\Administrator\\AppData\\Roaming\\npm\\clpwitnessd.cmd"
     }
   }
   ```
4. Register and start the service:
   ```sh
   winser -i -a
   ```
5. Verify in Control Panel → Administrative Tools → Services.
   ```sh
   Confirm that clpwitnessd-service exists in the service list.
   ```  

#### Linux
1. Create a working directory (e.g., `/opt/clpwitnessd`).
2. Create a systemd unit file `/etc/systemd/system/clpwitnessd.service`:
   ```ini
   [Unit]
   Description=EXPRESSCLUSTER Witness Server
   After=syslog.target network.target

   [Service]
   Type=simple
   ExecStart=/usr/bin/clpwitnessd
   WorkingDirectory=/opt/clpwitnessd
   KillMode=process
   Restart=always

   [Install]
   WantedBy=multi-user.target
   ```
3. Enable and start the service:
   ```sh
   systemctl enable clpwitnessd
   systemctl start clpwitnessd
   ```

## Step 5: Configure EXPRESSCLUSTER to Use the Witness Server
1. Open EXPRESSCLUSTER WebUI.
2. Select **Configuration Mode**.
3. Navigate to **Cluster Properties** → **Interconnect Tab**.
4. Click **Add** and select **Witness**.
6. Click on Properties and add witness Server settings
5. Configure the Witness Server settings:
   - **Target Host**: Set the host address of the Witness server.
   - **Service Port**: Define the port number.
   - **Use SSL**: Enable or disable SSL communication.
   - **Use Proxy**: Enable or disable proxy settings.
   - **HTTP Timeout**: Set the timeout for HTTP response.
   - Click **Initialize** to reset settings if needed.
6. Click **Apply** → **OK**.
7. Save the cluster configuration and switch to **Cluster Operation Mode**.

Now the Witness Server is successfully added to your EXPRESSCLUSTER environment.

For more information please refer :- [Reference Guide for the Witness Server](https://docs.nec.co.jp/software/clustering/expresscluster_x/x52/ecx_x52_windows_en/W52_RG_EN/W_RG_08.html#witness-server-service)
