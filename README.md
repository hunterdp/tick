# tick
How to install and get a simple TICK stack running with a Grafana frontend using Docker and Docker Compose.  

- This should not be used in production and is for learning purposes only.

Steps:

 a.  Create a local network for the stack to communicate on named tick-network.
	$ docker network create --driver bridge tick-network

 b.  The following ports will be exposed and used:
	8086	HTTP Svc
	8088	RPC backup & restore
	2003	Graphite service
	4242	OpenTSDB service
	8089	UDP service
	25826	collectd service

 c.  Setup persistent storage (use default locations for tick stack).  Mount
     local folders inside the containers that point to the default locations
     
	-v /Users/[userdir]/influxdb/data:/var/lib/influxdb
	-v /Users/[userdir]influxdb/config:/etc/influxdb

d.   The following is the docker command to run the latest influxdb
	$ docker run -d \
	   -- network tick-network \
	   -p 8086:8086 \
	   -p 8082:8082 \
	   -p 8089:8089 \
	   -v /Users/fprefect/influxdb/data/:/var/lib/influxdb \
	   -v /Users/fprefect/influxdb/config:/etc/influxdb \
	   --name influxdb \
           influxdb:1.5.4
     
