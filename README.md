# A Docker-based MapServer instance

This repository hosts a sample Docker-based MapServer setup. It uses
the MapServer image from [carletes/mapserver] and the [official Nginx
image]. It includes some of the map files and data from the [MapServer
tutorial], edited to use absolute paths.

## Running with Docker Compose

Install [Docker Compose](https://docs.docker.com/compose/install/) and
run the following command from the `docker-compose` directory:

    $ docker-compose up

You will then be able to access the following sample MapServer URLs:

* <http://localhost/mapserver/?map=example1-1.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-2.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-3.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-4.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-5.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-6.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-7.map&layers=all&mode=map>

## Running with Kubernetes

Install [Minikube](https://kubernetes.io/docs/getting-started-guides/minikube/)
and start the local Kubernetes instance. This step will take several
minutes:

    $ minikube start
	Starting local Kubernetes cluster...
	Starting VM...
	Downloading Minikube ISO
     89.51 MB / 89.51 MB [==============================================] 100.00% 0s
	SSH-ing files into VM...
	Setting up certs...
	Starting cluster components...
	Connecting to cluster...
	Setting up kubeconfig...
	Kubectl is now configured to use the cluster.
	$

Disable the default storage class:

    $ minikube addons disable default-storageclass
	default-storageclass was successfully disabled
	$

On a separate terminal, mount the sample mapserver data into the
Minikube VM:

    $ minikube mount $(pwd)/mapserver

Now load the Kubernetes deployment descriptors. First the
Minikube-specific ones:

    $ kubectl create -f k8s/minikube

Then the generic ones:

    $ kubectl create -f k8s/common

The components will take a while to load. You can monitor the progess
using the Kubernetes dashboard:

    $ minikube dashboard

Once the `mapserver` service is available, get its URL:

    $ export MAPSERVER_URL=$(minikube service --url mapserver)

You should now be able to access the following sample MapServer URLs:

    $ open ${MAPSERVER_URL}'/mapserver/?map=example1-1.map&layers=all&mode=map'
    $ open ${MAPSERVER_URL}'/mapserver/?map=example1-2.map&layers=all&mode=map'
    $ open ${MAPSERVER_URL}'/mapserver/?map=example1-3.map&layers=all&mode=map'
    $ open ${MAPSERVER_URL}'/mapserver/?map=example1-4.map&layers=all&mode=map'
    $ open ${MAPSERVER_URL}'/mapserver/?map=example1-5.map&layers=all&mode=map'
    $ open ${MAPSERVER_URL}'/mapserver/?map=example1-6.map&layers=all&mode=map'
    $ open ${MAPSERVER_URL}'/mapserver/?map=example1-7.map&layers=all&mode=map'

(Under Linux, use `xdg-open` instead of `open`).

[carletes/mapserver]: https://hub.docker.com/r/carletes/mapserver/
[official Nginx image]: https://hub.docker.com/_/nginx/
[MapServer tutorial]: http://mapserver.org/tutorial/index.html
