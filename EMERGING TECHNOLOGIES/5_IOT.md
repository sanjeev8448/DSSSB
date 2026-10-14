## 1. What is IoT?

The Internet of Things (IoT) is a network of physical objects embedded with sensors, software, processing capabilities, and connectivity that enables them to collect, exchange, and sometimes act on data.

Examples include smart watches, connected home appliances, industrial monitoring systems, and smart traffic lights.

### How IoT works

1. Sense

Sensors collect data from the environment

2. Connect

A network transfers the data

3. Process

A device, gateway, or cloud platform analyzes it

4. Act

An actuator or connected system performs an action, if needed

Example: A smart irrigation system measures soil moisture, sends readings to a controller, and switches on a water pump when the soil becomes too dry.

## 2. Sensors

A sensor is a device that detects a physical condition or change and converts it into a measurable signal.

Sensors provide the input data used by IoT systems.

### Common sensors

![Precision Digital Temperature & Humidity Sensor Module (DHT22) – Future Electronics Egypt](https://images.openai.com/static-rsc-4/pundR5bXvxyRblu209ZQi4T0qQcSbzd1jK3FWQNHj8WTAhiWLXmJLGrRqeBclENJGrn1WHii_sf1iFG5JTU9ZC7szyWD2wKOQtFW7qneJ2VCaw9wqx02OrriNSG2KDE9kHq4xcdL_2e2yKyE3i67k4xr3KSTnT32RSiMI9RrUwM?purpose=inline)

Temperature sensor

Measures temperature.

Example: Monitoring room temperature in a smart building.

![HC-SR04 Ultrasonic Module Distance Sensor | Ultrasonic Distance Sensor | Rapid Robotics Australia](https://images.openai.com/static-rsc-4/X3Xeum3GuwKwfRu_1OPJTxAS-SGQ8AgBKNhL0nGRXFbDts3nclleOR7ksdp1BC4vz8sClHIAtWd4zgiMtNEThw7bfNjoaXqXRd6NecE4KZgat_oY811HV_nCGgQpGiyHJSnwmNmx8ftiKjYj9ggv-IKo36AE-8vYnKFCBIyaiR8?purpose=inline)

Ultrasonic sensor

Measures distance using ultrasonic sound waves.

Example: Detecting obstacles in a parking system.

![LDR Sensor Module 3 Pin DC 3.3-5V Photoresistor Photo Cell Light Dependent Resistor LDR Sensor For Night Light Street Light Sensor Automatic Headlight Dimmer Control Photo Light Resistor](https://images.openai.com/static-rsc-4/Bb_lBQqkoILQoyEZ-gCL27vDUrEnSthUw9Qk9qkZI-SEpGYv4T0ScjZUyWnAakl34cBD-P1mbIjVo3tis7Dzh-GheVXY6LqejpdtIBIj2jdGq1uNvD-cvM80hv_sw2Q4PjGrPFFt1NcfB6SGWGbGbJFa2WW-rJmRFwviSLIsJn0?purpose=inline)

Light sensor (LDR)

Detects light intensity.

Example: Automatically switching streetlights on when it gets dark.

![Senzor vlhkosti půdy Botland - obchod s robotikou](https://images.openai.com/static-rsc-4/uaU92upUFtLznncCTtkAdveQMSwe21JUI4cu2QzjSMr0ITKYxiYLqTKHb6lgNPSij9tFUJ3nGaFonrDGVBCjk2qovnkpx2Jfd929ul4pjY08ylZuq7-boOx_RNbLPauhV_FIXISSRS_v4voM0-zrFxrN3zLYS8WRCP4qPk7v0IA?purpose=inline)

Soil-moisture sensor

Measures soil moisture.

Example: Automated irrigation.

Other examples include motion sensors (PIR), pressure sensors, gas sensors, accelerometers, and heart-rate sensors.

Exam point: A sensor measures or detects a condition; it does not necessarily perform a physical action.

## 3. Actuators

An actuator is a device that converts a control signal or energy into a physical action.

While sensors collect information, actuators help an IoT system respond to that information.

### Common actuators

|Actuator|Function|IoT example|
|---|---|---|
|Motor|Produces rotational movement|Smart fan or robotic wheel|
|Servo motor|Controls angular position|Automatic door mechanism|
|Relay|Electrically switches a circuit|Turning a pump on or off|
|Solenoid valve|Opens or closes fluid flow|Smart irrigation|
|Buzzer|Produces sound|Intruder alarm|
|LED|Produces light|Smart lighting|

### Sensor vs actuator

|Sensor|Actuator|
|---|---|
|Detects or measures|Performs an action|
|Provides input|Produces an output or physical response|
|Example: Temperature sensor|Example: Cooling fan|
|Example: Soil-moisture sensor|Example: Water pump|

Example: In an automatic cooling system, a temperature sensor detects heat, the controller evaluates the reading, and a relay or motor controller activates the fan.

## 4. IoT connectivity

Connectivity allows IoT devices to exchange information with other devices, gateways, servers, or cloud platforms.

### Common connectivity technologies

|Technology|Typical use|Key point|
|---|---|---|
|Wi-Fi|Smart appliances, cameras|Relatively high data rates; often higher power consumption than low-power IoT alternatives|
|Bluetooth Low Energy (BLE)|Wearables, nearby sensors|Short-range and energy-efficient|
|Zigbee|Smart-home sensors and lighting|Low-power mesh networking|
|RFID|Identification and tracking|Uses radio waves to identify tagged objects|
|NFC|Contactless interactions|Very short-range communication|
|LoRaWAN|Remote environmental sensors|Long-range, low-power, low-data-rate communication|
|Cellular (4G/5G, LTE-M, NB-IoT)|Connected vehicles and remote devices|Uses cellular infrastructure; capabilities vary by technology|
|Ethernet|Industrial and fixed installations|Wired connectivity|

### Communication protocols

Protocols define how devices exchange data.

- MQTT: Lightweight publish-subscribe messaging protocol often used in IoT.
    
- HTTP/HTTPS: Web communication protocols used for APIs and device-cloud communication.
    
- CoAP: Lightweight web-transfer protocol designed for constrained devices and networks.
    

### IoT network structure

A typical setup is:

IoT device → Gateway or network → Internet/cloud platform → Application

A gateway may collect data from local devices, translate protocols, filter information, or forward data to the cloud. Some devices connect directly to the internet without a separate gateway.

## 5. IoT applications

![Smarte Lichtsysteme & -steuerung entdecken | MediaMarkt](https://images.openai.com/static-rsc-4/yOI-uJpWVbL867x5cxZL8hfPklLqfqHcHLtxyJRkcfXAYwqWPQm5pH4-ONnIjZExyFa2ljiHRI5WLszoX3d_4LNveTMdNmH40ECuVgQBXoBJC7XZKTJDGmYwKNVVOfBtpcadsGzeO59qvpNOCkA7HM8fOnO_u4SGWasNPQUWZMU?purpose=inline)

Smart homes

Connected lights, thermostats, locks, and appliances can be monitored and controlled remotely.

![Predictive Maintenance (PdM)](https://images.openai.com/static-rsc-4/gmq7j0-79VCOXWEilRdQw_dT2V88FBmf3ii-o5mvF14OYLxIgKX2a0fsLbwxx7TM5vmKotNV-ZvCasviG29bLGrbeWU5uhjLpvAS7SEGtkP9vEzaolIB9iYPbAtSfDUXG9a9u4YakW88nizcmVc1r4CtWKFO4ynyTM8U-kgTHqo?purpose=inline)

Industrial IoT (IIoT)

Sensors monitor machine temperature, vibration, and performance to support fault detection and predictive maintenance.

![Modern Irrigation & Water Technology — AquaLinked Media](https://images.openai.com/static-rsc-4/rFIvpbV_Hs1SWq9LPoskzo5B2u9ccNCjNiuMnqWg5DkgU-t_th-xq7XFx1u0FJsXiKrxKuH4R9WQBIzJ33ozaanIjQqLZRBB99xp7_WIzqrKlmui2QKFiHuP4T5cO_ni-IhZy3PkDzowlXlhKPPMJodr2MWwmM0Tgc6vFl3434U?purpose=inline)

Smart agriculture

Soil sensors, weather data, and automated irrigation help optimize water usage and crop monitoring.

![SpO2 Monitoring for Athletes India | Pulse Oximeter for Gym India](https://images.openai.com/static-rsc-4/vr-fXibzaVxt83SdwPK9BnBVVCPRghTJRXV5_c90Hc-b1tlW3C5ro5hcJFN51za4OSCi-5fZc1Fu9-1AlLUY1gvNy3m3MbHdcQkJdLWC9xFD8YPVfE6JZEgmhGQC5r8KrQDeJ1xNVDtJh5ZYoQ29X32jsoNRpSfAusznHS4TnoU?purpose=inline)

Healthcare

Wearables and connected medical devices can monitor health-related measurements and transmit data to healthcare systems.

## 6. Smart cities

A smart city uses connected devices, sensors, communication networks, and data analysis to improve urban services, resource use, safety, and sustainability.

### Important smart-city applications

![วิสัยทัศน์ พันธกิจ ยุทธศาสตร์](https://images.openai.com/static-rsc-4/GJbZfnU64xPCUpRdNNmkj8R21GEnUQqbQ3_Lyp9zjuCDUhi94-4ZLctD9VGsWaF5ZjA6nkLFq67e7EqYjJPAQjPZY1bXptdDpvAXGyaZdJnNeEMbGsramQP3ZPrdFraDKH7E286422CC5FYuRJcPjtjpxaD1U9wdhvUe7dd8Wng?purpose=inline)

Smart traffic management

Traffic sensors monitor vehicle flow, helping systems adjust signal timings and identify congestion.

![Intelligent Street Lighting | Mindteck](https://images.openai.com/static-rsc-4/1qh9uqTR3idZZF-U7bjPtdMpJx2BnDdyykUkDPZqzMyW1jWatrKBunrMfoCm4ra7pgmhM-N2eC9uXKK77J9AOr47J94e2xCignJBzH3zvzGr80IVDtmaibF67psh59mMPRvnFN8FtaLalTdWEuWhxIJJNtcHXz8Po-OpNs2FCqE?purpose=inline)

Smart streetlights

Light and motion sensors help control streetlights and reduce unnecessary energy consumption.

![Waste Management and Prediction of Air Pollutants Using IoT and Machine Learning Approach | MDPI](https://images.openai.com/static-rsc-4/eR4ViEIWaNGoms0TfitNw0ilGg-0gY8BS5dg8uB8QP6HoGFSSOTVlhruiFUTAtn9u--gaA0fLJXV9GstTU5HzYg3P6Ootsbocw7aOt3hz8hQe8bqe8Jt_LE8b6qBwfpJBIB0SrmEVPer7chfgkbdP9EnvTq9uRW2Rz3XmH5Zbwk?purpose=inline)

Smart waste management

Fill-level sensors help prioritize waste collection routes.

![Solar Air Quality Monitoring Station | Off-Grid AQMS](https://images.openai.com/static-rsc-4/XmUREHK9e-dbY26Xck-EDlfCyEtMiqxtk5HXMCi8EtjMRil1uDNRDA6PM9wy4ZtiudsJN3FExhPVYKrhZHUsR3SGfwxS0TaiEhvyDGQfDYpcdn6qbMOitHpJcEnMxgIHR67twA2Xc-9EjpLI4p2qO7rANNGaAz0vLhvmlhG-XOI?purpose=inline)

Environmental monitoring

Connected sensors measure air quality, noise, temperature, or water conditions.

Benefits: Better resource utilization, improved service delivery, reduced energy waste, and data-driven planning.

Challenges: Cybersecurity, privacy, interoperability, network reliability, and installation and maintenance costs.

## 7. IoT architecture basics

IoT architecture describes the layers or components through which devices collect data, communicate, process information, and provide services.

A common introductory model has three layers.

### 3. Application layer

Dashboards, alerts, smart-home apps, traffic monitoring

### 2. Network layer

Wi-Fi, cellular, gateways, routing, data transfer

### 1. Perception layer

Sensors, RFID, actuators, physical-world interaction

Data commonly travels upward; control commands can travel downward. The exact layer names vary across architecture models.

### Three-layer architecture explained

|Layer|Main responsibility|Example|
|---|---|---|
|Perception|Detects physical conditions and interacts with the environment|Temperature sensor|
|Network|Transfers data between devices, gateways, and services|Wi-Fi or cellular network|
|Application|Provides services to users or other systems|Smart irrigation dashboard|

Some models use a five-layer architecture, adding processing/middleware and business layers. For an introductory exam question, identify which architecture the question describes rather than assuming every IoT model has exactly three layers.

### Worked example: Smart irrigation

1. Perception: A soil-moisture sensor measures soil conditions.
    
2. Network: Readings are sent to a controller or cloud service.
    
3. Application/processing: The system checks whether the soil is too dry.
    
4. Action: A controller activates a relay to operate the water pump.
    

### Important IoT challenges

- Security: Prevent unauthorized access to devices and data.
    
- Privacy: Protect personal or sensitive information.
    
- Interoperability: Allow devices from different vendors to work together.
    
- Power consumption: Extend battery life for remote devices.
    
- Scalability: Support growing numbers of connected devices.

## Last-minute revision

- Sensor: Detects or measures.
    
- Actuator: Performs a physical action.
    
- Connectivity: Wi-Fi, BLE, Zigbee, LoRaWAN, cellular, and Ethernet.
    
- Smart cities: Traffic, streetlights, waste, and environmental monitoring.
    
- Three-layer architecture: Perception → Network → Application.
    
- MQTT: Lightweight publish-subscribe messaging.
    
- Main challenges: Security, privacy, interoperability, power, and scalability.