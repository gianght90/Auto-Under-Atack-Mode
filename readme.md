# CloudFlare Under Attack Mode Automation

### What does it do
This is a bash script designed to automate the process of enabling and disabling Cloudflare's Under Attack Mode based on CPU load percentage using the Cloudflare API.  This can be a lifesaver when you're dealing with DDoS attacks or other high-load situations.

### How to install

Navigate to the parent path where you want to install.  If you want to install to
/home/cfautouam then navigate to /home

```bash
cd /home
wget https://raw.githubusercontent.com/gianght90/Auto-Under-Atack-Mode/master/cfautouam.sh;
```
config: cf_email, cf_apikey, cf_zoneid, maincf_zoneid, upper_cpu_limit, lower_cpu_limit, regular_status, regular_status_s, time_limit_before_revert

```bash
mkdir cfautouam;
cp cfautouam.sh cfautouam/cfautouam.sh
cd cfautouam;
chmod +x cfautouam.sh;
./cfautouam.sh -install;
```

It's now installed and running from the defined parent path, check the logs and confirm it's working.  You can delete the original file.

After confirming it works, set debug level to 0.


### Command Line Arguments
```
-install        : installs and enables service
-uninstall      : uninstalls and then deletes the sub folder
-disable_script : temporarily disables the service from running
-enable_script  : re-enables the service
-enable_uam     : enables Under Attack Mode manually
-disable_uam    : disables Under Attack Mode manually
```

### Notes
This script was designed to run out of it's own separate folder, if you change that you may have problems.

### TODO
* Add more accurate CPU usage function
* Add error checking to command line arguments

Frequently Asked Questions
--------------------------

**Cloudflare's Under Attack Mode (UAM) - What is it?**

Cloudflare's UAM is a protective feature designed to shield your site from DDoS attacks. When activated, it presents an interstitial page to your site's visitors. During this time, Cloudflare is busy analyzing the visitor's traffic to ensure it's legitimate.

**CPU Load Thresholds - What are they?**

These are the levels of CPU load that trigger the script to either enable or disable UAM. The CPU load is a percentage representation of your server's total capacity. For instance, if you set the upper threshold at 35, the script will switch on UAM when your server's CPU load goes beyond 35%.

**Regular Security Level - What does this mean?**

This refers to the security level that Cloudflare will default to when UAM is not active. You have the freedom to set this to any of Cloudflare's security levels, which include: "off", "essentially off", "low", "medium", or "high".

**Time Limit before Reverting from UAM - What's this about?**

This is a set minimum duration that the script will observe before it disables UAM after it has been enabled. This mechanism is in place to avoid quick toggling between states if your CPU load is hovering around the upper limit.

**Installing the Script as a Service - How do I do this?**

You can make the script a service by executing it with the -install argument. This action will generate a systemd service and timer that run the script at regular intervals.

**Uninstalling the Script - How is this done?**

To uninstall the script, you need to run it with the -uninstall argument. This will halt and disable the systemd service and timer, and also delete the script's files from your server.

**Manually Enabling or Disabling UAM - How can I do this?**

To manually switch on UAM, you need to run the script with the -enable_uam argument. Conversely, to switch it off, use the -disable_uam argument.
