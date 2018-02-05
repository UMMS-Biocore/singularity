BootStrap: docker
From: ubuntu:16.04

%labels

    AUTHOR Alper Kucukural <alper.kucukural@umassmed.edu>
    Version v1.0

%post
    apt-get update
    apt-get -y upgrade
    apt-get dist-upgrade
    apt-get -y install libsqlite3-dev libbz2-dev libssl-dev python python-dev \
    python-pip git libxml2-dev software-properties-common wget tree vim \
    subversion g++ gcc gfortran libcurl4-openssl-dev curl

    echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
    add-apt-repository -y ppa:webupd8team/java && \
    apt-get update && \
    apt-get install -y oracle-java8-installer && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/oracle-jdk8-installer

    apt-get -y autoremove

    export JAVA_HOME=/usr/lib/jvm/java-8-oracle
    mkdir /data && cd /data
    curl -s https://get.nextflow.io | bash 
    mv /data/nextflow /usr/bin/.

    mkdir /project /nl /share /.nextflow

    export GITUSER=UMMS-Biocore

    git clone https://github.com/${GITUSER}/dolphin-bin /usr/local/bin/dolphin-bin

    pip install -U boto
    pip install numpy
    pip install RSeQC

    cd /usr/local/bin/dolphin-bin/MACS2 && python setup.py install
    make -C /usr/local/bin/dolphin-bin/RSEM-1.2.29

    echo "export PATH=$PATH:/bin:/sbin:/usr/local/bin/dolphin-bin" >> "/environment"

