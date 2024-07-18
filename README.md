## Wordpress in kubernetes

This repository provides Kubernetes configuration files to deploy a WordPress application.These configuration files allow you to easily deploy a WordPress application with a MySQL database on a Kubernetes cluster.
Files

All the files needed to deploy Wordpress in kubernetes are given below
Configmap.yaml

In this file YAML code defines a Kubernetes ConfigMap named “mysql-config” that stores configuration data for a MySQL database. Here’s a brief explanation:

    - apiVersion and kind specify that this is a ConfigMap resource.
    - metadata provides metadata about the ConfigMap, including its name “mysql-config”.
    - data contains the configuration data as key-value pairs:
        - DATABASE: “bawa” (database name)
        - USER: “bawa” (database user)
        - PASSWORD: “bawa1234” (database password)
        - ROOT_PASSWORD: “bawa0056” (database root password)

## Mysql_deployment.yaml

This depolyment file is defines the MySQL database deployment. Explanation of code is given below:-

   - Kind: Deployment (type of resource)
   -  Metadata: labels and name for the deployment
   - Spec:
       - Replicas: 1 (number of pods to run)
       - Selector: matches pods with label “app: mysql”
       - Template:
           - Metadata: labels for the pod
           - Spec:
               - Containers:
                   - Env: environment variables for the container (database name, user, password, root password) from the ConfigMap “mysql-config”
                   - Image: mysql:5.7 (docker image to use)
                   - Name: db (container name)
                   - Ports: 3306 (container port)

## Mysql_service.yaml

This YAML code defines a Kubernetes Service named “mysql” that exposes a MySQL database pod. Here’s a brief explanation:

    apiVersion and kind specify that this is a Service resource.
    metadata provides metadata about the Service, including its name “mysql”.
    spec defines the Service’s specifications:
        ports: exposes port 3306 (default MySQL port)
        selector: matches pods with label “app: mysql” (selects the MySQL pod to expose)

In short, this Service exposes the MySQL pod’s port 3306, making it accessible within the Kubernetes cluster.

## Wordpress_deployment.yaml

In wordpress deployment file given manifest defines Kubernetes Deployment named “wp” that runs a WordPress container. Here’s a brief explanation:

    Kind: Deployment (type of resource)
    Metadata: labels and name for the deployment
    Spec:
        Replicas: 1 (number of pods to run)
        Selector: matches pods with label “app: wordpress”
        Strategy: empty (default strategy)
        Template:
            Metadata: labels for the pod
            Spec:
                Containers:
                    Env: environment variables for the container (database host, user, password, name) from the ConfigMap “mysql-config”
                    Image: wordpress:5.2 (docker image to use)
                    Name: wordpress (container name)
                    Ports: 80 (container port)

In short, this Deployment runs a single pod with a WordPress container, using environment variables from a ConfigMap to connect to a MySQL database.

## wordpress_service.yaml

The code in this file explain the following things:-
This code creates a Kubernetes Service named “wordpress” that:

    Exposes port 80
    Selects pods labeled “app: wordpress”
    Uses a LoadBalancer for external access

In short, it exposes WordPress on port 80, making it accessible from outside the cluster.

## Steps for project:-
run these commands in local terminal
   1.git clone repository name
   2.kubectl apply -f directory-name
