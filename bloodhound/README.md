# bloodhound

## Overview

BloodHound uses graph theory to reveal the hidden and often unintended relationships within an Active Directory or Azure environment. Attackers can use BloodHound to easily identify highly complex attack paths that would otherwise be impossible to quickly identify. Defenders can use BloodHound to identify and eliminate those same attack paths. Both blue and red teams can use BloodHound to easily gain a deeper understanding of privilege relationships in an Active Directory or Azure environment.


## Installation and First Setup

    curl -L https://ghst.ly/getbhce -o docker-compose.yml
    docker compose pull && docker compose up

    get the first time password from the container logs and go to http://127.0.0.1:8080 login with user 'admin' and the password and reset the password

    Then do
    git clone https://github.com/dirkjanm/BloodHound.py -b bloodhound-ce
    to clone the bloodhound-python ingestor for the bloodhound-ce

    Then do pip install . to install the bloodhound.py dependencies

    And run it with
    python bloodhound.py

## Usage Bloodhound-python

    -d <domain_name> : specifies the domain name
    -c <type> : type of information to be collected
    -ns <target_ip> : name server

    --zip : compresses the json output into a zip file



## Usage Bloodhound

First we need to use https://github.com/BloodHoundAD/SharpHound or https://github.com/dirkjanm/BloodHound.py for data collection:

    bloodhound-python -d <domain_name> -c all -u <username> -p <password> -ns <target_ip> --zip

If we are in a windows machine, logged in a a user, but with now password, we can download the sharphound.exe and run it in the context of the user

    ./sharphound.exe -c all

Using sharphound is better since more up to date

Then, start bloodhound by doing

    docker compose -f - up -d

In the dir with the bloodhound compose file

Now that we have collected the data go to http://127.0.0.1:8080/ui/administration/file-ingest and upload the zip created by bloodhound-python

After the status of the ingested data changes to complete go to http://127.0.0.1:8080/ui/explore

# More Information

https://github.com/SpecterOps/BloodHound