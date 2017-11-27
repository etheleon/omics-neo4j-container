# Omics neo4j docker image

This repository provides the necessary Dockerfile to set up the container environment (neo4j v2.2.3) to load
graph database built with [omics](github.com/etheleon/omics) for my PhD dissertation.

You'll need to have [Docker](https://docs.docker.com/engine/installation/) installed.

## Download Docker Image

After installing Docker, pull the image:

```
docker pull etheleon/omics-neo4j-container
```

## Download DB, Decrypt, Decompress run Docker

Download the DBs using the links provided below expires in 1 year in Dec 2018. Please approach me for the passphrase to decrypt the gz files.

### Simulation

1. Initial analysis with Single Copy Gene KOs only
    * Contigs compared with trimmed NR db [contigs_against_trimmednr](https://thesis-neo4j-db.s3.amazonaws.com/sim/contigs_against_trimmednr.tar.gz.gpg?AWSAccessKeyId=AKIAJ5SH5HHDXK4UI5GA&Signature=xG6YgNR7upoABqdVB2rM4pIiGsQ%3D&Expires=1511766540)
    * Contigs compared with NR db [full NR](https://thesis-neo4j-db.s3.amazonaws.com/sim/contigs_against_fullnr.tar.gz.gpg?AWSAccessKeyId=AKIAJ5SH5HHDXK4UI5GA&Signature=4yTreye%2BZmGkq4bDE%2BvEHYvkYIk%3D&Expires=1511766540)

```
LINK="https://s3-ap-southeast-1.amazonaws.com/thesis-neo4j-db/sim/allKOS_fullnr.tar.gz.gpg" contigs_against_trimmednr.tar.gz.gpg"
curl -O -L $LINK
```

2. With all KOs
    * Contigs compared with trimmed NR db [trimmed NR](https://thesis-neo4j-db.s3.amazonaws.com/sim/allKOS_trimmednr.tar.gz.gpg?AWSAccessKeyId=AKIAJ5SH5HHDXK4UI5GA&Signature=Y8sdO7mQWT1g%2Fcw%2FeiM18Q9LiiE%3D&Expires=1511766540)
    * Contigs compared with NR db [full NR](https://thesis-neo4j-db.s3.amazonaws.com/sim/allKOS_fullnr.tar.gz.gpg?AWSAccessKeyId=AKIAJ5SH5HHDXK4UI5GA&Signature=a%2BBv0J8wFLye%2BowHRRiZCFBzJgg%3D&Expires=1511766540)

### Ulu Pandan

1. Initial analysis with Single Copy Gene KOs [trimmed NR](), [full NR]()
2. With all KOs [trimmed NR](), [full NR]()

### Perturbation


### Time-series

Once you've downloaded the file rename it to <name>.tar.gz.gpg

```
DB=<DBname>
#DB=allKOS_fullnr
gpg --yes --batch --passphrase=[Enter your passphrase here] $DB.tar.gz.gpg
tar -zvxf $DB.tar.gz
```

```
#Run the Docker container
data=$PWD/$DB
docker run \
    --name omics
    --publish=7474:7474 --publish=7687:7687 \
    --volume=$data:/data \
    etheleon/docker-neo4j-publish:latest
```



