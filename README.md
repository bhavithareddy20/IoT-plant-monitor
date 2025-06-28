# IoT-plant-monitor
# Send DHT22 data with ESP32 using MQTT to Node-Red Dashboard


## Flow diagram of the Project

<img src="./esp32mqttdht22_github.svg" width=100% height=40%>

### Step 1: Install the Required Libraries
- Open an Arduino IDE --> Tools --> Manage Libraries
- Search and install the following libraries
    
    pubsubclient
    WiFi
    DHT sensor library for ESPx
    

### Step 2: Hardware Schematic
- Four pin DHT22
<img src="./DHT22_esp32.png" width=40% height=40%>

### Step 3: Running the program
- Copy the code to the Arduino IDE
- Setup the Board and Port
- Connect the ESP32 to the USB port of the computer
- Upload the code
- Monitor the values in the Serial monitor

### Step 4: Setup the Node-RED flow

- Open Node-RED URL in the browser
- Click on Menu --> Manage Palette
- Search for "node-red-dashboard" and install it. 
- Import the flow using the following code


[
  {
    "id": "5e04b9dd.81c658",
    "type": "tab",
    "label": "MQTT Dashboard",
    "disabled": false,
    "info": ""
  },
  {
    "id": "6ec4dcef.913b24",
    "type": "mqtt-broker",
    "name": "",
    "broker": "broker.hivemq.com",
    "port": "1883",
    "clientid": "",
    "autoConnect": true,
    "usetls": false,
    "protocolVersion": "4",
    "keepalive": "15",
    "cleansession": true
  },
  {
    "id": "6f670e80.d2e0f",
    "type": "ui_tab",
    "name": "Dashboard",
    "icon": "dashboard",
    "order": 1
  },
  {
    "id": "92a9cd27.99b9d",
    "type": "ui_group",
    "name": "Sensor Readings",
    "tab": "6f670e80.d2e0f",
    "order": 1,
    "disp": true,
    "width": "6",
    "collapse": false
  },
  {
    "id": "mqtt-temp",
    "type": "mqtt in",
    "z": "5e04b9dd.81c658",
    "name": "",
    "topic": "iotfrontier/temperature",
    "qos": "2",
    "datatype": "auto-detect",
    "broker": "6ec4dcef.913b24",
    "x": 130,
    "y": 100,
    "wires": [["debug-temp", "chart-temp"]]
  },
  {
    "id": "mqtt-hum",
    "type": "mqtt in",
    "z": "5e04b9dd.81c658",
    "name": "",
    "topic": "iotfrontier/humidity",
    "qos": "2",
    "datatype": "auto-detect",
    "broker": "6ec4dcef.913b24",
    "x": 130,
    "y": 160,
    "wires": [["debug-hum", "gauge-hum"]]
  },
  {
    "id": "mqtt-soil",
    "type": "mqtt in",
    "z": "5e04b9dd.81c658",
    "name": "",
    "topic": "iotfrontier/soil",
    "qos": "2",
    "datatype": "auto-detect",
    "broker": "6ec4dcef.913b24",
    "x": 130,
    "y": 220,
    "wires": [["debug-soil", "gauge-soil"]]
  },
  {
    "id": "debug-temp",
    "type": "debug",
    "z": "5e04b9dd.81c658",
    "name": "Temp Debug",
    "active": true,
    "tosidebar": true,
    "console": false,
    "tostatus": false,
    "complete": "payload",
    "targetType": "msg",
    "x": 320,
    "y": 80,
    "wires": []
  },
  {
    "id": "debug-hum",
    "type": "debug",
    "z": "5e04b9dd.81c658",
    "name": "Hum Debug",
    "active": true,
    "tosidebar": true,
    "console": false,
    "tostatus": false,
    "complete": "payload",
    "targetType": "msg",
    "x": 320,
    "y": 140,
    "wires": []
  },
  {
    "id": "debug-soil",
    "type": "debug",
    "z": "5e04b9dd.81c658",
    "name": "Soil Debug",
    "active": true,
    "tosidebar": true,
    "console": false,
    "tostatus": false,
    "complete": "payload",
    "targetType": "msg",
    "x": 320,
    "y": 200,
    "wires": []
  },
  {
    "id": "chart-temp",
    "type": "ui_chart",
    "z": "5e04b9dd.81c658",
    "name": "Temperature",
    "group": "92a9cd27.99b9d",
    "order": 1,
    "width": 0,
    "height": 0,
    "label": "Temperature",
    "chartType": "line",
    "legend": "false",
    "xformat": "HH:mm",
    "interpolate": "linear",
    "nodata": "",
    "dot": false,
    "ymin": "0",
    "ymax": "50",
    "removeOlder": 1,
    "removeOlderPoints": "",
    "removeOlderUnit": "3600",
    "cutout": 0,
    "useOneColor": false,
    "useUTC": false,
    "colors": ["#ff9900"],
    "outputs": 1,
    "useDifferentColor": false,
    "x": 330,
    "y": 100,
    "wires": [[]]
  },
  {
    "id": "gauge-hum",
    "type": "ui_gauge",
    "z": "5e04b9dd.81c658",
    "name": "Humidity",
    "group": "92a9cd27.99b9d",
    "order": 2,
    "width": 0,
    "height": 0,
    "gtype": "gage",
    "title": "Humidity",
    "label": "%",
    "format": "{{value}}",
    "min": 0,
    "max": "100",
    "colors": ["#00b3d9", "#0073e6", "#001bd7"],
    "seg1": "33",
    "seg2": "66",
    "diff": false,
    "className": "",
    "x": 330,
    "y": 160,
    "wires": []
  },
  {
    "id": "gauge-soil",
    "type": "ui_gauge",
    "z": "5e04b9dd.81c658",
    "name": "Soil Moisture",
    "group": "92a9cd27.99b9d",
    "order": 3,
    "width": 0,
    "height": 0,
    "gtype": "gage",
    "title": "Soil Moisture",
    "label": "%",
    "format": "{{value}}",
    "min": 0,
    "max": "100",
    "colors": ["#00e400", "#ffff00", "#ff0000"],
    "seg1": "33",
    "seg2": "66",
    "diff": false,
    "className": "",
    "x": 330,
    "y": 220,
    "wires": []
  }
]
- Deploy the flow
- Navigate to the following URL and modify the <your IP address>. For example http://localhost:1880/ui

http://<your IP address>:1880/ui

- Monitor the values in the Dashboard as below
  
<img src="./nodered-dashboard-humidity-temp.png" width=40% height=40%>
