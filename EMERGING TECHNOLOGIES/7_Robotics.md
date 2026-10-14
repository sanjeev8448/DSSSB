## 1. Robot basics

Definition: A robot is a programmable machine that can perform tasks automatically or semi-autonomously using control systems, sensors, and actuators.

Robots may be controlled by a computer program, a human operator, or a combination of both.

### Main components of a robot

![Robotics # Kinematic Chains. Welcome to this comprehensive guide on… | by Dilip Kumar | Medium](https://images.openai.com/static-rsc-4/tsGa-CYKgPRvfZOJyK_NSx_SqLvMiO1IaqaHHrAjBSKVRu-U3lpBg00PokYNrjMLTtAh8rrxonDkFvLdfQMy1JVjH_6amqY8dkZbtnEq575Sy61xzCbvB6eHpIISK-KmWeTVy1pfxrHKQZjS1xCEHp98OR_bjLko3yRRHA5dc4A?purpose=inline)

1. Mechanical structure

The physical body, frame, joints, wheels, or arms that provide movement and support.

![Freenove 4WD Robot Car Kit with Line Following, Obstacle Avoidance...](https://images.openai.com/static-rsc-4/5sH4S0j0zBTlHI7owDfYmrfjDPjCCtikY7ycVcEUYvJ7dMm6z5B39Fz1UXZqUguIe2INQ2VdQhP1PnNkU2iO6Snr0HIFZHOv6YnuHZwIaRmqLcrQMk-euVzNESHjKCyrFHFWzju5aa6DlaPRmC2s5BHcgfShFsstKGDe2xoX4iU?purpose=inline)

2. Sensors

Collect information about the surroundings or the robot's own condition, such as distance, temperature, and position.

![KRS-5033HV ICS 伺服馬達(六入組) -QTS 品測科技](https://images.openai.com/static-rsc-4/F6Pl8hXOTut6LEqg92iXXSsWN5L9ie-ZVYHoWxnMnRnmol6A41jmhHE-qotW-8TSdGNDFNxHEqrFXWf7IRex4gJLqAmWr5cbvTgorBOUAOI2hbMbMPNL4fw4iGplUm--Dso7-RY3xcz059iPmUvT_bawh3TjZbqMLqemQcUUwys?purpose=inline)

3. Actuators

Convert energy into physical movement, such as rotating a wheel or moving a robotic arm.

![Adeept Robot Control Board Compatible with Arduino IDE | Smart Car Control Board | MEGA328P](https://images.openai.com/static-rsc-4/weKMOQ-aSDaP6hUOBI04R9JceIFl2gqbqIw3JETG5HPStOSeim4E-VxLQRRKqv4Qc0MS3xfJyT7KeDoTMI4SEOBWYrh_6npImOaOev8K96BDDpD9CJNm4pAAcUzaTrR3fIz_gz8SUsvOY7lKza4AZYAZMc8Y8sMi7LpXq2rRfv0?purpose=inline)

![Adeept Robot Control Board Compatible with Arduino IDE | Smart Car Control Board | MEGA328P](https://images.openai.com/static-rsc-4/weKMOQ-aSDaP6hUOBI04R9JceIFl2gqbqIw3JETG5HPStOSeim4E-VxLQRRKqv4Qc0MS3xfJyT7KeDoTMI4SEOBWYrh_6npImOaOev8K96BDDpD9CJNm4pAAcUzaTrR3fIz_gz8SUsvOY7lKza4AZYAZMc8Y8sMi7LpXq2rRfv0?purpose=inline)

4. Controller

Processes sensor inputs, executes control logic, and sends commands to actuators.

5. Power supply

Provides the energy required by the controller, sensors, and actuators.

Provides the energy required by the controller, sensors, and actuators.

### How a robot works

A typical robot follows a feedback loop:

1. Sense: Sensors collect information.
    
2. Process: The controller interprets the information and decides what to do.
    
3. Act: Actuators perform the required movement or action.
    
4. Repeat: Sensors measure the result, allowing the controller to adjust its behavior.
    

Example: A mobile robot detects an obstacle, processes the distance reading, and turns its wheels to avoid a collision.

### Important robot types

|Type|Description|Example|
|---|---|---|
|Industrial robot|Performs repetitive manufacturing tasks|Robotic welding arm|
|Mobile robot|Moves through an environment|Warehouse delivery robot|
|Humanoid robot|Has a human-like body or features|Human-shaped service robot|
|Collaborative robot (cobot)|Designed to work alongside people with appropriate safety measures|Assembly assistant|
|Autonomous robot|Performs tasks with some independent decision-making|Robotic floor cleaner|

Exam point: Not every robot is autonomous. Some robots require continuous human control.

## 2. Sensors used in robotics

A sensor detects or measures a physical condition and provides information to the robot's controller.

Sensors help robots navigate, detect objects, maintain balance, measure their position, and interact safely with their environment.

|Sensor|What it detects|Example in robotics|
|---|---|---|
|Ultrasonic|Distance using sound waves|Obstacle avoidance|
|Infrared (IR)|Infrared radiation; often used for proximity or line detection|Line-following robot|
|Camera / vision sensor|Images and visual information|Object recognition|
|LiDAR|Distance and surroundings using laser light|Robot navigation and mapping|
|Touch / force sensor|Contact or applied force|Robotic gripping|
|Temperature sensor|Temperature|Monitoring industrial equipment|
|Gyroscope|Angular velocity|Balance and orientation control|
|Accelerometer|Acceleration and changes in motion|Detecting tilt or movement|
|Encoder|Rotation or displacement of a motor or joint|Measuring wheel movement|
|GPS / GNSS receiver|Geographic position outdoors|Outdoor delivery robots|

### Important distinctions

- Ultrasonic sensor: Uses sound waves to measure distance.
    
- Infrared sensor: Uses infrared radiation; the exact function depends on the sensor design.
    
- LiDAR: Uses laser light to measure distances and construct environmental maps.
    
- Camera: Captures images for visual processing.
    
- Encoder: Measures rotational movement or position; it is not the same as a camera or proximity sensor.
    

### Sensor vs actuator

|Sensor|Actuator|
|---|---|
|Collects information|Performs an action|
|Input to the control system|Output from the control system|
|Example: Distance sensor|Example: Motor|
|Detects an obstacle|Moves the robot away from it|

## 3. Applications of robotics

![Čak 25 posto velikih poduzeća u EU koristi robote](https://images.openai.com/static-rsc-4/MDE80h69wD4POWILG3XMG_RMgb_FI7FNgQ8F1rxdpjuAz2u7TDX0f_JVlwlhrMpglMh9ZUBn2gsMUIyTollYRyySF5VeXuQnM8JV0JF0krtMXl28jTyGGTfdu1-9KJOYNa0Wdsp4gr-ZDhOGJicOvwUCBUI_ugJgcF-Asa6rswM?purpose=inline)

Manufacturing

Welding, painting, assembly, packaging, and repetitive precision tasks.

![هل يخطئ الطبيب؟  الذكاء الاصطناعي يرى ما لا تراه العين فى الأشعة التشخيصية - أموالي منصة الناشرين](https://images.openai.com/static-rsc-4/4KBqWmS8aaxx0GcAHaBZ_oVFv2ARPKz9FtRWJPZwg411yOUVamyZ0tukKRRq1sDTv2K2BEQ8xUeB7aO0wOgHfWi6Wh1nwVxyXFMTh0wpT0GjwJBntcFKRyaNvL7Us9N41oaFM5imIS9dWhxW20O678ucRJt7_O4IGWhbPkNqkO8?purpose=inline)

Healthcare

Robot-assisted procedures, rehabilitation, laboratory automation, and hospital logistics.

![AI in Logistics: Benefits, Use Cases & Practices | GEP Blog](https://images.openai.com/static-rsc-4/wmr-wUZn74qZ-8NZ6RI4DAM6RrS4EicN2CG--Dq3mRkE5RW3oiiUpa82_a-tBAsoZicuapELPz9U0P1oSox-g8OGInZBoXkgm-X2cFshDd2YZdnamIfPE03YgnAwK_9steg1lACJxSTE9GWbNcyhIciRk0ccHnXJqjkiZp49n48?purpose=inline)

Warehousing and logistics

Moving goods, sorting packages, and transporting inventory.

![AgRobotics demos set for Ontario | The Grower](https://images.openai.com/static-rsc-4/1PLUKQEONdV0UsE1FM3dkw8JRHLapa-nYdEMkxESuimWLbqroou8HWva4kR4qehkcpqhucDJ3BOk6ee9ZRldKeXCy06S2-Fg5zCPOSbs5jfjmO1Y2wFIVv5z3YJ9VLsw2NgsbpsrBFILiHr9BFsETBn_kG-KiURu83S4_Zg9_cw?purpose=inline)

Agriculture

Crop monitoring, targeted spraying, planting, and harvesting.

![Life on Mars? Meet the new rover built to give us the answer | Space](https://images.openai.com/static-rsc-4/kFpNT-N80ntzbkFb5rsnkQNsUWls2dv31_y2Pgmr0p9mVfZTZMMKCk4CRLADdN724bJ7FdhwKqzJXCPkeZ4Jyl3HcJf5rXJ0ufRmxcLqDVtAh0nn5jQ3Euw2FFphXjgN2qAOx-Mmb0z_620zbbtPDjCtYDSgdh5NPuCUXZ1wcgs?purpose=inline)

Space and hazardous environments

Exploring planets, inspecting dangerous locations, and handling radioactive or toxic materials.

![SENCOR SRV 9185BK Robot Vacuum and Mop Instruction Manual](https://images.openai.com/static-rsc-4/MJ7_XsmcCPEvCmzXCGKQhc6h4xFxYwNFq_UJGF51QPYbvJsDs2nkT9_4ruMoIIVIkUbpjCm7kEPzrL1lOMyA1a87jTTE4hGTuFCPSwHYhFIbrGjW4CdZZrEa8RVH7HVtCu2N62Y_3ExbU3OjnaeQETgrCTTKTAwIkHef3ZMSSQc?purpose=inline)

Domestic and service robots

Cleaning, lawn mowing, assistance, and other household tasks.

### Benefits and limitations

Benefits

- High precision and repeatability.
    
- Can perform dangerous or physically demanding tasks.
    
- Can operate continuously when properly maintained.
    
- Can improve productivity and consistency.
    

Limitations

- Initial purchase and maintenance costs.
    
- Dependence on power, sensors, and software.
    
- Safety risks if systems malfunction.
    
- Difficulty handling unfamiliar situations without suitable sensing and control.
### Last-minute revision

- Robot: Programmable machine that performs tasks automatically or semi-autonomously.
    
- Sensor: Detects or measures.
    
- Actuator: Produces physical action.
    
- Controller: Processes information and coordinates actions.
    
- Ultrasonic: Distance using sound waves.
    
- LiDAR: Distance measurement using laser light.
    
- Encoder: Measures rotation or displacement.
    
- Applications: Manufacturing, healthcare, agriculture, logistics, space exploration, and domestic tasks.