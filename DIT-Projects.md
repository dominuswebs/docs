# Local server deployment ( media player in office )

    # Lineup exporter ( PDF, PNG )
        In progress

    # Schematic generator
        Waiting approval

    # Store previewer

    # Profisee previewer

    # localserver

    # PM2

    # basic usage
    $ npm install pm2 -g
    $ pm2 start server.js

    # you can even define how many processes you want in cluster mode:
    $ pm2 start server.js -i 4

    # you can start various processes, with complex startup settings
    # using an ecosystem.json file (with env variables, custom args, etc):
    $ pm2 start ecosystem.json


    # credentials

    ubuntu
        User dit_user
        Pass ubuntuserver

    Sftp
        User sftpuser
        Pass ubuntusftp

    # Wifi password update

    navigate to configuration folder
    $ cd /etc/netplan
    open installer file and edit wifi interface name / password
    $ sudo nano XX-installer-config.yaml 
    apply changes
    $ sudo netplan apply


    # office server

    IP - 10.0.0.87

    # copy files

    scp username@remote_host:/path/to/remote/file /path/to/local/directory

# Framework repository

    # Product code report

    # Asset report

# New framework

    # GUI (JSON configuration)

    # New assets
        Export x5 from figma - consistent scale
    
    # Simplified module system 
        No more feasts, boxes, a la carte

        Only text, asset, group, section with variants

        Variables - $CODE is replaced by the code, $PRICE and so on

        Import saved groups, sections - ex: save a box lineup and reuse it

        Conditions - if, switch
            
            Combine condition checks ( is date and is tag)

        Sync and animation timeline
            Trigger animations in child files - main file triggers rotation in LTO file for example

        Reload
            Trigger reload to rerender screen, not a new page request

