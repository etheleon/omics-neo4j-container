# Omics neo4j docker image

This repository provides the necessary Dockerfile to set up the container environment (neo4j v2.2.3) to load
graph database built with [omics](github.com/etheleon/omics) mentioned in PhD dissertation.

You'll need to have [Docker](https://docs.docker.com/engine/installation/) installed.

## Download Docker Image

After installing Docker, pull the image:

```
docker pull etheleon/omics-neo4j-container
```

## Download DB
Download the DBs using the links provided below expires in 1 year in Dec 2018. Please approach me for the passphrase to decrypt the gz files.

### Simulation

1. Initial analysis with Single Copy Gene KOs only
    * Contigs compared with trimmed NR db [contigs_against_trimmednr](https://s3-ap-southeast-1.amazonaws.com/thesis-neo4j-db/sim/contigs_against_trimmednr.tar.gz.gpg)
    * Contigs compared with NR db [full NR](https://s3-ap-southeast-1.amazonaws.com/thesis-neo4j-db/sim/contigs_against_fullnr.tar.gz.gpg)

2. With all KOs
    * Contigs compared with trimmed NR db [trimmed NR](https://s3-ap-southeast-1.amazonaws.com/thesis-neo4j-db/sim/allKOS_trimmednr.tar.gz.gpg)
    * Contigs compared with NR db [full NR](https://s3-ap-southeast-1.amazonaws.com/thesis-neo4j-db/sim/allKOS_fullnr.tar.gz.gpg)

### Ulu Pandan

1. Initial analysis with Single Copy Gene KOs [trimmed NR](), [full NR]()
2. With all KOs [trimmed NR](), [full NR]()

### Perturbation


### Time-series

## Decrypt, Decompress


```
DB=allKOS_fullnr
#decrypt
gpg --yes --batch --passphrase=[Enter your passphrase here] $DB.tar.gz.gpg
#gunzip and untar
tar -zvxf $DB.tar.gz
```

##  Run Docker

```
#Run the Docker container
data=$PWD/$DB
docker run \
    --name omics
    --publish=7474:7474 --publish=7687:7687 \
    --volume=$data:/data \
    etheleon/docker-neo4j-publish:latest
```

