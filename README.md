There are 6 static BaderLab static websites.  Each site is in a stand alone virtual machine running old software.  This repo is the documentation on the new versions of these old static websites.

The websites are:
1. POW (pow.baderlab.org) - 192.168.81.143
2. PRM-DB (prm-db.org) - 192.168.81.192
3. pathguide (pathguide.org) - 192.168.81.175
4. DV-IMPACT (dvimpact.baderlab.org / canvd.baderlab.org) - 192.168.81.189
5. MIMP (mimp.baderlab.org) - 192.168.81.141
6. cytoscape wiki (wikiold.cytoscape.org) - 192.168.81.131

Each site has been converted over to a docker and is now running newer versions of software.  All servers are running on ubuntu OS.

The corresponding dockers are:
1. POW - [iweinberger/pow](https://hub.docker.com/repository/docker/iweinberger/pow/general)
2. PRM-DB - [iweinberger/prm-db](https://hub.docker.com/repository/docker/iweinberger/prm-db/general)
3. pathguide - [iweinberger/pathguide](https://hub.docker.com/repository/docker/iweinberger/pathguide/general)
5. DV-IMPACT - [iweinberger/dv-impact](https://hub.docker.com/repository/docker/iweinberger/dv-impact/general)
6. MIMP - uncompleted
7. cytoscape wiki - uncompleted

Each docker can be downloaded and run through Docker user the command `docker run -ditp 80:80 **container_name**`

POW:
This site 
