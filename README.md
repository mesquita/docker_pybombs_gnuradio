# Docker to install GNU Radio 3.8 via Pybombs
A Dockerfile to install GNU Radio via Pybombs that works in 2021 (with Ubuntu 20.04 and Python 3.8.5 and GNU Radio 3.8), differently from all the other stuff that I am seeing throughout the internet.

This might not be the best Dockerfile ever, but gets the job done. I encourage everyone to upgrade it to their needs.

To build the container:
```
$  docker build -f Dockerfile -t docker_pybombs_gnuradio .
```

To run the container, I am using this right now (it let you run the GNU Radio GUI and use the USRPs via USB).

```
$ xhost +
$ SOCK=/tmp/.X11-unix
$ XAUTH=/tmp/.docker.xauth
$ xauth nlist $DISPLAY | sed -e 's/^..../ffff/' | xauth -f $XAUTH nmerge -
$ chmod 777 $XAUTH
$ docker run -ti --privileged -e DISPLAY=$DISPLAY \
        -v `pwd`/../:/docker_pybombs_gnuradio \
        -v /dev/bus/usb:/dev/bus/usb \
        -v $XSOCK:$XSOCK -v $XAUTH:$XAUTH -e XAUTHORITY=$XAUTH --net host docker_pybombs_gnuradio
```

Enjoy it.