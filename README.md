# A Docker-based MapServer instance

This repository hosts a sample Docker-based MapServer setup. It uses
the MapServer image from [carletes/mapserver] and the [official Nginx
image]. It includes some of the map files and data from the [MapServer
tutorial], edited to use absolute paths.



## Running

Install [Docker Compose](https://docs.docker.com/compose/install/) and
run the following command from the top-level directory:

    $ docker-compose up

You will then be able to access the following sample MapServer URLs:

* <http://localhost/mapserver/?map=example1-1.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-2.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-3.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-4.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-5.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-6.map&layers=all&mode=map>
* <http://localhost/mapserver/?map=example1-7.map&layers=all&mode=map>

[carletes/mapserver]: https://hub.docker.com/r/carletes/mapserver/
[official Nginx image]: https://hub.docker.com/_/nginx/
[MapServer tutorial]: http://mapserver.org/tutorial/index.html
