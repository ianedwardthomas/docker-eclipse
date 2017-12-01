Docker Eclipse
==============

Installation
------------

1. Install recent version of docker engine and docker compose ([docker.com]())

2. Build the image:

        docker-compose  build

3. Prepare your own copy of the configuration:

                cp env .env

3. Run the image:

        docker-compose  up -d

4. Connect using a VNC client to port 5901

Usage
-----

5. You should be able to run the command in ```/home/ubuntu/eclipse-installer/eclipse-inst``` to install eclipse and then run it.

6. State is kept in ```eclipseuserdata``` volume.
