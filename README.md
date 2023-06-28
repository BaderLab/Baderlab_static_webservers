There are 6 static BaderLab static websites.  Each site is in a stand alone virtual machine running old software.  This repo is the documentation on the new versions of these old static websites.

The websites are:
1. POW (pow.baderlab.org) - 192.168.81.143
2. PRM-DB (prm-db.org) - 192.168.81.192
3. pathguide (pathguide.org) - 192.168.81.175
4. DV-IMPACT (dvimpact.baderlab.org / canvd.baderlab.org) - 192.168.81.189
5. MIMP (mimp.baderlab.org) - 192.168.81.141
6. cytoscape wiki (wikiold.cytoscape.org) - 192.168.81.131

Each site has been converted over to a docker and is now running newer versions of software.  All servers are running on ubuntu OS and using APT for package managment.

The corresponding dockers are:
1. POW - [iweinberger/pow](https://hub.docker.com/repository/docker/iweinberger/pow/general)
2. PRM-DB - [iweinberger/prm-db](https://hub.docker.com/repository/docker/iweinberger/prm-db/general)
3. pathguide - [iweinberger/pathguide](https://hub.docker.com/repository/docker/iweinberger/pathguide/general)
5. DV-IMPACT - [iweinberger/dv-impact](https://hub.docker.com/repository/docker/iweinberger/dv-impact/general)
6. MIMP - uncompleted
7. cytoscape wiki - [iweinberger/cytoscape-wiki-old](https://hub.docker.com/repository/docker/iweinberger/cytoscape-wiki-old/general)

Each docker can be downloaded and run through Docker user the command `docker run -ditp 80:80 **container_name**`.
Each site has it's own Docker image however all 6 sites have also been combined into one docker image which can be found at iweinberger/all-baderlab-sites(https://hub.docker.com/repository/docker/iweinberger/all-baderlab-sites/general)

POW:
  POW is a website that allows users to predict PDZ domain-peptide interactions for human, mouse, worm and fly PDZ domains.
  Software:
  - python2.7
  - svm
  - apache2
  - apache2 cgi

PRM-BD:
  PRM-DB allows users to search for a domain or protein by name, all domains from a given species, all members of a domain family, or search for combinations of these criteria.
  Software:
  - apache2
  - mySQL
  - PHP
  - php-mysql
  - libapache2-mod-php

DV-IMPACT:
  DV-IMPACT is a resource for the disease variants impact assessment on domain-peptide PPI networks
  Software:
  - apache2
  - mySQL
  - PHP
  - php-mysql
  - libapache2-mod-php

Pathguide:
  Pathguide is a database that contains information about 702 biological pathway related resources and molecular interaction related resources
  - apache2
  - mySQL
  - PHP
  - php-mysql
  - libapache2-mod-php

MIMP:
  MIMP characterizes genetic variants such as cancer mutations that specifically alter kinase-binding sites in proteins.
  Software:
  - List incomplete (coming soon)

Cytoscape wiki (old):
  Old wiki for cytoscape.
  - apache2
  - python2
  - MoinMoin
  - libapache2-mod-wsgi-py3
