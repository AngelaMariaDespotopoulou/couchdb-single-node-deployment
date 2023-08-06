# CouchDB Deployment (Single-node Configuration)
**CouchDB** is an open-source, [NoSQL](https://en.wikipedia.org/wiki/NoSQL) database management system designed to store and manage large amounts of data efficiently. Developed by the [Apache Software Foundation](https://www.apache.org/), CouchDB is built upon a document-oriented data model, making it a part of the family of document databases. It stores data in [JSON](https://en.wikipedia.org/wiki/JSON)-like documents, making it highly flexible and schema-free, allowing easy adaptability to changing data requirements. One of CouchDB's distinguishing features is its robust replication and synchronization capabilities, enabling seamless data synchronization across multiple nodes and devices. This makes it ideal for distributed and decentralized applications, enabling offline data access and real-time collaboration. With its [RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer) [API](https://en.wikipedia.org/wiki/API) and support for [MapReduce](https://en.wikipedia.org/wiki/MapReduce) views, CouchDB provides powerful querying capabilities. It is an excellent choice for applications requiring scalability, fault tolerance, and reliable data synchronization in a distributed environment.

This repository contains all the necessary materials and instructions to easily deploy a CouchDB service using [Docker](https://www.docker.com/) in a **single-node** configuration for development purposes. It includes a built-in administration user interface called **Fauxton** (formerly Futon) accessible via HTTP.

## Instructions
1. Clone the present [Git](https://en.wikipedia.org/wiki/Git) repository.

1. Navigate to the source directory.

1. Configure the variables in the [.env](.env) file and save changes.

1. Build the Docker image and start a container simultaneously by typing:    
    ```
    docker-compose -f couchdb-single-node.yml -p couchdb up -d
    ```

1. Test by accessing via your browser the address: 
    ```
    http://<hostname>:<http_port>/
    ```
    Default configuration:
    ```
    http://localhost:5984/
    ```

1. Access the Fauxton user interface at:
    ```
    http://<hostname>:<http_port>/_utils/
    ```
    Default configuration:
    ```
    http://localhost:5984/_utils/
    ```

1. Login using the credentials you configured in the [.env](.env) file.

## Cleaning up
1. Run the following command to stop the container:
    ```
    docker-compose -f couchdb-single-node.yml -p couchdb down
    ```

1. To clean unused images, networks and volumes you may execute (**at your own risk**):
    ```
    docker system prune -a
    ```

## Notes
1. Unless configured otherwise, the data of the database will be placed in the [data](data) directory of the present repository.
1. Do not leave the [.env](.env) file unattended on a cloud server as it contains hardcoded passwords.
1. The default **HTTP** port of CouchDB v3.0 is **5984**, while the **HTTPS** one is **6984**. (Ports 4369 and 9100-10 are used in cluster configurations.)
1. **CouchDB** has nothing to do with [Couchbase](https://en.wikipedia.org/wiki/Couchbase_Server) even though their names are similar. 
1. [Spring Framework](https://spring.io/) and [Spring Boot](https://spring.io/projects/spring-boot) do not have built-in support for CouchDB out of the box via Spring Data, for instance. Therefore, [Java](https://www.java.com/en/) developers have two options:
* To just perform HTTP calls on the database by leveraging its REST API.
* To use **[Ektorp](https://helun.github.io/Ektorp/reference_documentation.html)**, a Java library that provides support for integrating CouchDB with Spring Framework applications.

## Useful External Links
* [Official Documentation for CouchDB 3.0](https://docs.couchdb.org/en/stable/index.html)
* [Official Documentation for Fauxton UI](https://couchdb.apache.org/fauxton-visual-guide/)
* [GitHub Repo for CouchDB open-source project](https://github.com/apache/couchdb)
* [DockerHub Repo for CouchDB](https://hub.docker.com/_/couchdb)