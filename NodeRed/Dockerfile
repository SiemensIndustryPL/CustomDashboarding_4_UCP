FROM nodered/node-red:latest-18-minimal
WORKDIR /usr/src/node-red/
USER root
COPY package.json .
COPY custom_nodes/ .
RUN npm install --unsafe-perm --no-update-notifier --no-fund --only=production
RUN npm install node-red-contrib-influxdb
RUN npm install node-red-contrib-postgresql
RUN npm install node-red-contrib-s7
#
# Your custom node installations go here
# use RUN npm install <node-red-nodename>
#
CMD ["npm", "start", "--", "--userDir", "/cfg-data"] 

