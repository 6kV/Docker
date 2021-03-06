Containers :
-------------

    zookeeper:
      image: garland/zookeeper
      ports:
        - "2181:2181"
        - "2888:2888"
        - "3888:3888"
    mesosmaster:
      image: garland/mesosphere-docker-mesos-master
      ports:
        - "5050:5050"
      links:
        - zookeeper:zk
      environment:
        - MESOS_ZK=zk://zk:2181/mesos
        - MESOS_LOG_DIR=/var/log/mesos
        - MESOS_QUORUM=1
        - MESOS_REGISTRY=in_memory
        - MESOS_WORK_DIR=/var/lib/mesos
    marathon:
      image: garland/mesosphere-docker-marathon
      links:
        - zookeeper:zk
        - mesosmaster:master
      command: --master zk://zk:2181/mesos --zk zk://zk:2181/marathon
      ports:
        - "8080:8080"
    mesosslave:
      image: garland/mesosphere-docker-mesos-master:latest
      ports:
        - "5051:5051"
      links:
        - zookeeper:zk
        - mesosmaster:master
      entrypoint: mesos-slave
      environment:
        - MESOS_HOSTNAME=192.168.33.10
        - MESOS_MASTER=zk://zk:2181/mesos
        - MESOS_LOG_DIR=/var/log/mesos
        - MESOS_LOGGING_LEVEL=INFO
