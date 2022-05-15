# MavPi
An ARCH64 image for the RaspberryPi 3b-4b/Zero 2 sporting both QGroundControl and MissionPlanner

As this image is development ready it's pretty large, the download link is below.
All passwords are set to default (pi/raspberry) so be sure to update them after you flash.
SSH is enabled by default so access should be pretty straightforward.
WIFI can be enabled by altering the /etc/wpa_supplicant/wpa_supplicant.conf file and adding something like the following:
network={
        ssid="mynetwork"
        psk="mypassword"
}
I have provided the most basic of window managers (DWM) as when using mono windows resizing just wasn't working out.
Everything is setup to automatically launch at startup, just edit the /home/pi/start_mav.sh file with whatever options suit your needs:

        export SES_TYPE="SSH"
        if [ $XDG_SESSION_ID == 1 ]; then
                export SES_TYPE="CONSOLE"
                export DISPLAY=:0.0
                # These are some memory handling experiments.
                # export MALLOC_MMAP_THRESHOLD_=450
                # export MALLOC_ARENA_MAX_1
                startx &
                cert-sync /etc/ssl/certs/ca-certificates.crt # This will keep our mono certificates valid.
                sleep 5
                xrandr -d :0 --output HDMI-1 --rotate right  # Rotate screen (adjust to your needs).
                # /usr/bin/mp &  # Launch MissionPlanner.
                # /bin/QGroundControl &  # Launch QGroundControl.
        fi
        echo SESSION_TYPE-------------------------------------------------------------------: $SES_TYPE
        env  # Dump the environment so we can see whats up in the event of a failure.

This image is in a working but entirely untested state, MissionControl is the latest version and will run under mono. Alternatively QGroundControl is also at the latest version and has been compiled without error (Take note that AirMap was excluded as I just couldn't get it to plat ball).
All sources and notes are located in /usr/src.

Have Fun!

<download link here>
