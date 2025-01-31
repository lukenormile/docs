# Add to an Existing System

You can add REMnux to an existing system based on Ubuntu 20.04 by following instructions below. This configuration doesn't modify your system's look and feel, so you won't have the experience of the full REMnux environment. To the full experience, consider using the [REMnux virtual appliance](get-virtual-appliance.md).

{% hint style="info" %}
REMnux is based on an x86/amd64 version of Ubuntu, and won't run on an ARM processor such as Apple M1.
{% endhint %}

## Step 1: Get the REMnux Installer <a href="#get-remnux-installer" id="get-remnux-installer"></a>

After logging into your existing system based on Ubuntu 20.04, download the REMnux installer:

```
wget https://REMnux.org/remnux-cli
```

Validate that the SHA-256 hash of the downloaded file to make sure it matches this expected value:

```
23c7f4eefa7599ea2c4156f083906ea5fd99df18f306e4bb43eec0430073985a
```

To generate the hash of your  file, run:

```
sha256sum remnux-cli
```

Set up the REMnux installer by running these commands:

```
mv remnux-cli remnux
chmod +x remnux
sudo mv remnux /usr/local/bin
```

Before proceeding, make sure your system doesn't have an active Ubuntu unattended upgrade in progress. One way to do this is check whether the "unattended-upgrade" process is active (`ps aux | grep unattended-upgrade`.) If the upgrade is active, let it finish or [disable it](https://askubuntu.com/questions/1098757/ubuntu-18-10-unattended-upgrades-shutdown-wait-for-signal#1099258), then reboot the system before installing REMnux.

## Step 3: Run the REMnux Installer <a href="#run-remnux-installer" id="run-remnux-installer"></a>

You're now ready to install the REMnux distro. To kick off the installation, run:

```
sudo remnux install --mode=addon
```

The `addon` mode will avoid modifications that can modify the look and feel of your existing system. As a result, you won't get the experience of the standard REMnux environment..

The installation will take about an hour, depending on your resources and internet connection.

{% hint style="info" %}
If the REMnux installer produces an error, diagnose the issue by reviewing the saltstack.log file under /var/cache/remnux/cli in the subdirectory that matches the REMnux state-files version you're installing. Search for the log file for `result: false` messages and look at the surrounding 5 lines or the 8 lines above each message to see the state file that caused the issue. (`grep -i -C 5 'result: false'` or `grep -i -B 8 'result: false'`).
{% endhint %}

## Step 4: Reboot the  REMnux System <a href="#reboot-remnux" id="reboot-remnux"></a>

Once the REMnux installation finishes, reboot your new REMnux system by typing:

```
sudo reboot
```

Login to your system to start benefiting from the tools that the REMnux distro includes.

{% hint style="success" %}
To keep your REMnux environment up-to-date run the REMnux installer periodically as described in the [Keep the Distro Up to Date](keep-the-distro-up-to-date.md) section.
{% endhint %}

## Step 5: Take a Snapshot of the Virtual Machine <a href="#take-snapshot" id="take-snapshot"></a>

If you installed REMnux inside a virtual machine, consider taking a snapshot of the VM, so you can return it to a known good state if the need arises.
