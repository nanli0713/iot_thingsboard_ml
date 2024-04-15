# iot_smart_classroom

#### Introduce
This project is mainly based on thingsboard and realizes the combination of machine learning and thingsboard. python: First use the code to randomly generate 1000 rows of data and save it to a csv file. Then use three methods: linear regression, decision tree regression and random forest regression to simulate training and testing. Finally, we got the best simulation model: random forest . Deep learning MLP is also used for simulation, with an accuracy rate as high as 99%.thingsboard: Use python to dynamically display temperature, humidity, and brightness data on thingsboard. If the student's efficiency is less than 60%, an alarm will be issued.

#### Software Architecture
```
Smart Classroom based on thingsboard and python
|
|————README.md //Chinese document
|————README.en.md //English document
|————data    // Mock data simulated by python, output as csv file
|    └————student_efficiency_environment.csv
|————output    // Image path output by machine learning
|    |————model_performance_plots.png    // ML Model Simulated image
|————iot_lab5.ipynb  // Contains mock data generation code, ML data simulation code, and thingsboard connection code
|————iot-dl.ipynb  // DL data simulation code with an accuracy rate of up to 99%
└————thingsboard // Folder containing pictures of various configurations of thingsboard
```

thingsboard


#### Environmental preparation

1.  Use your own email address to register an account on the thingsboard official website. At this time, you will have a trial period of about one month. The website address is as follows: https://thingsboard.cloud/dashboards/all
2.  The project is modified based on the official Smart Office dashboard, so a lot of your work is to modify its demo.
3.  My computer: macbook 2020 air m1
4.  python environment：python=3.11.5,pandas==2.0.3,numpy==1.26.4,json==2.0.9,sklearn==1.3.0,matplotlib==3.7.2,requests==2.31.0
5.  torch：2.2.2+cuda121
6.  nvidia-smi:
 <img width="840" alt="截屏2024-04-15 13 03 41" src="https://github.com/nanli0713/iot_thingsboard_ml/assets/77238981/c76d5fef-d243-4104-9aad-0269f0a93b9b">

#### Thingsboard configuration (Extremely important)

1. First, you have to install the smart office template

   ![截屏2024-04-11 14.11.48](./thingsboard/截屏2024-04-11_14.11.48.png)

   ![截屏2024-04-11 14.11.48](./thingsboard/截屏2024-04-11_14.12.52.png)

2. Then I modified it step by step to the smart classroom I wanted.

![截屏2024-04-11 14.15.40](./thingsboard/截屏2024-04-11_14.15.40.png)

Remove the HVAC switch and the indicator below it:

![截屏2024-04-11 14.16.40](./thingsboard/截屏2024-04-11_14.16.40.png)

Delete the configurations related to Energy Meter, Water Meter and HVAC in Office Devices in the Entity alias of the computer phone icon in the upper right corner, leaving only one Smart Sensor:

- Click the Entity alias of the computer phone icon in the upper right corner
- Modify the last Device Type in Office Devices, leaving only one Smart Sensor

![截屏2024-04-11 14.24.41](./thingsboard/截屏2024-04-11_14.24.41.png)

![截屏2024-04-11 14.26.07](./thingsboard/截屏2024-04-11_14.26.07.png)

![截屏2024-04-11 14.26.18](./thingsboard/截屏2024-04-11_14.26.18.png)

- Now we only have one smart sensor that needs to be modified, and this smart sensor has its own dashboard, which we also need to modify.
- Therefore, we first click on the Smart sensor row or the small triangle icon in Devices in the smart office dashboard to enter the dashboard. Click save first to enter.

![截屏2024-04-11 14.28.56](./thingsboard/截屏2024-04-11_14.28.56.png)

![截屏2024-04-11 14.30.57](./thingsboard/截屏2024-04-11_14.30.57.png)

- Then you can continue to modify various indicators in the smart sensor, for example, delete some data that is not in my classroom:

![截屏2024-04-11 14.32.48](./thingsboard/截屏2024-04-11_14.32.48.png)

- Then you add some data you need. For example, I need temperature, humidity, lightness and final student learning efficiency in my smart classroom.
- So I directly copied the temperature card in the upper right corner and found that all the variables, colors and units were the same, so I needed to modify these variables again.

#### ![截屏2024-04-11 14.36.07](./thingsboard/截屏2024-04-11_14.36.07.png)

![截屏2024-04-11 14.37.18](./thingsboard/截屏2024-04-11_14.37.18.png)

So most of you just need to modify the theme and unit, and of course the data source.

- Modify units

![截屏2024-04-11 14.38.04](./thingsboard/截屏2024-04-11_14.38.04.png)

- Modify name

<img src="./thingsboard/截屏2024-04-11_14.38.26.png" alt="截屏2024-04-11_14.38.26" style="zoom:50%;" />

- Modify colors

![截屏2024-04-11 14.38.26](./thingsboard/截屏2024-04-11_14.40.34.png)

- Therefore

![截屏2024-04-11 14.39.35](./thingsboard/截屏2024-04-11_14.39.35.png)

- By analogy, after saving, you will modify the contact info. These variables are all integrated in the attributes of Office under assert. You can modify them to your own email and address, etc. Then do not delete this floorPlan. This is strongly related to the map component in your smart office dashboard

![截屏2024-04-11 14.45.54](./thingsboard/截屏2024-04-11_14.45.54.png)

- After the modification is completed, you can modify the picture in the upper right corner of the dashboard homepage

![截屏2024-04-11 14.49.27](./thingsboard/截屏2024-04-11_14.49.27.png)

- I will modify it into a picture of student learning efficiency. You can click edit to modify the data source.

![截屏2024-04-11 14.51.01](./thingsboard/截屏2024-04-11_14.51.01.png)

- When modifying, we found that there is no data source for student efficiency, so we need to create a new one:

![截屏2024-04-11 14.52.37](./thingsboard/截屏2024-04-11_14.52.37.png)

Then we delete the second data source and keep the newly created data source:

![截屏2024-04-11 14.53.26](./thingsboard/截屏2024-04-11_14.53.26.png)

As before, we need to modify the data type and unit of the ordinate of this picture. I will change it to efficiency, %.

![截屏2024-04-11 14.54.26](./thingsboard/截屏2024-04-11_14.54.26.png)

Finish：

![截屏2024-04-11 14.55.41](./thingsboard/截屏2024-04-11_14.55.41.png)



![截屏2024-04-11 14.56.37](./thingsboard/截屏2024-04-11_14.56.37.png)



![截屏2024-04-11 14.57.04](./thingsboard/截屏2024-04-11_14.57.04.png)



![截屏2024-04-11 14.57.16](./thingsboard/截屏2024-04-11_14.57.16.png)

Click save to save the project.

- Before testing the code, we also need to modify the telemetry variables of the smart-sensor device.

![截屏2024-04-11 15.03.49](./thingsboard/截屏2024-04-11_15.03.49.png)

It is not difficult to find that many variables are no longer useful, and I also need to add lightness and efficiency

- Next, we modify the latest telemetry of the smart sensor

![截屏2024-04-11 15.05.50](./thingsboard/截屏2024-04-11_15.05.50.png)

- Let’s try to see if we can use the https protocol and use python to make data post requests.

The code is as follows: (You need to modify it according to the ipynb file)

```python
import os
import requests
import json 
import time
headers = {
    'Content-Type': 'application/json',
}
# Loop through each row of data
for index, row in df.iterrows():
    # 取出对应列的数据
    temperature = round(float(row['温度']),2)
    humidity = round(float(row['湿度']),2)
    lightness = round(float(row['光亮度']),2)
    efficiency = round(float(row['学习效率'])*100,2)
    data_telemetry = {"temperature": temperature,"humidity": humidity,"lightness":lightness,"efficiency":efficiency}#initialization
    data_telemetry = json.dumps(data_telemetry)
    requests.post('https://thingsboard.cloud/api/v1/your_device_id/telemetry', headers=headers, data=data_telemetry)
    print(f"Temperature: {temperature}, Humidity: {humidity}, lightness: {lightness}, Efficiency: {efficiency}")
    time.sleep(5)#wait 5 seconds to sent the next data
    
```

If nothing else, you only need to modify **https://thingsboard.cloud/api/v1/your device number/telemetry** and replace the device number in the middle with your real smart sensor device number:

-The device number is here:

![截屏2024-04-11 15.07.39](./thingsboard/截屏2024-04-11_15.07.39.png)

Click on the small shield icon behind the smart sensor and you will get the device number.

#### ![截屏2024-04-11 15.08.18](./thingsboard/截屏2024-04-11_15.08.18.png)

After the connection is successful, you will find that these values ​​are moving:

![截屏2024-04-11 15.09.28](./thingsboard/截屏2024-04-11_15.09.28.png)

And your device is also in active state:

![截屏2024-04-11 15.10.16](./thingsboard/截屏2024-04-11_15.10.16.png)

- If you click smart_sensor in devices in smart office, you will find that these charts are changing dynamically, which means that our data transmission is successful!

![截屏2024-04-11 15.11.40](./thingsboard/截屏2024-04-11_15.11.40.png)

- According to the picture above, I don’t find that the data of the lightness card is not quite right. Let’s reset its threshold:

![截屏2024-04-11 15.13.46](./thingsboard/截屏2024-04-11_15.13.46.png)

![截屏2024-04-11 15.13.58](./thingsboard/截屏2024-04-11_15.13.58.png)

ok，everything is fine!

- student efficiency is also displayed normally

![截屏2024-04-11 15.21.46](./thingsboard/截屏2024-04-11_15.21.46.png)

- Now, we need to modify the rules of alarms: Since alarms are generated based on the previous rules, according to our smart classroom vision, we need to use students’ learning efficiency as the final criterion, so if the learning efficiency is low Alarm at 50%:

- The modified page has alarm rules in the smart-sensor of device profiles

![截屏2024-04-11 15.24.21](./thingsboard/截屏2024-04-11_15.24.21.png)

- after modified：

![截屏2024-04-11 15.26.13](./thingsboard/截屏2024-04-11_15.26.13.png)

So we have this low efficiency warning

![截屏2024-04-11 15.31.59](./thingsboard/截屏2024-04-11_15.31.59.png)

- Add a logical chain, although it may not be useful:

![截屏2024-04-12_14.29.33](./thingsboard/截屏2024-04-12_14.29.33.png)

![截屏2024-04-12_14.29.42](./thingsboard/截屏2024-04-12_14.29.42.png)

![截屏2024-04-12_14.29.53](./thingsboard/截屏2024-04-12_14.29.53.png)

![截屏2024-04-12_14.30.05](./thingsboard/截屏2024-04-12_14.30.05.png)

![截屏2024-04-12_14.30.17](./thingsboard/截屏2024-04-12_14.30.17.png)
#### Screenshot of the final perfect project

![截屏2024-04-11 15.31.59](./thingsboard/截屏2024-04-11_16.32.49.png)
![截屏2024-04-11 15.31.59](./thingsboard/截屏2024-04-11_16.33.26.png)
![截屏2024-04-11 15.31.59](./thingsboard/截屏2024-04-11_16.46.46.png)

#### Python code description
##### 1.Generate random numbers
##### 2.Save to csv file for easy reading
![截屏2024-04-12_14.30.17](./thingsboard/截屏2024-04-12_14.51.43.png)
##### 3. Use machine learning methods for model fitting
- Divide the data set into 80% training set and 20% test set

- Use three machine learning methods for simulation: Linear Regression, Decision Tree, Random Forest
![截屏2024-04-12_14.30.17](./thingsboard/截屏2024-04-12_14.52.26.png)
- Plot simulation results
![截屏2024-04-12_14.30.17](./output/model_performance_plots.png)
- Evaluate the performance of three models using MSE and MAE
- draw final conclusions
![截屏2024-04-12_14.30.17](./thingsboard/截屏2024-04-12_14.52.43.png)
##### 4. Use deep learning methods for model fitting
- Divide the data set into 80% training set and 20% test set
- Simulation using deep learning method: MLP multi-layer perceptron
- Simulation results: the accuracy rate reached over 99%
- data reading
![截屏2024-04-12_14.30.17](./thingsboard/截屏2024-04-15_13.08.10.png)
- Model construction
![截屏2024-04-12_14.30.17](./thingsboard/截屏2024-04-15_13.08.30.png)
- result：
![截屏2024-04-12_14.30.17](./thingsboard/截屏2024-04-15_13.08.42.png)
##### 5.connect thingsboard
- Send data such as temperature, humidity, brightness and student learning efficiency to smart-sensor

- View the printing information of requests
![截屏2024-04-12_14.30.17](./thingsboard/截屏2024-04-12_14.52.53.png)

#### author

- City University Of Hongkong Li Yinan LiYinan
- email: 17856560989@163.com
- If you have any questions related to the project, you can send me an email to ask. My ability is limited, so please criticize and correct me.

#### Quote

- https://thingsboard.io/use-cases/smart-office/

