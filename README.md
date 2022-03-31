# SKU-SEN0291-Gravity-I2C-Digital-Wattmeter-SEN0291
Chapter 3 code_Project_78 The second part 2 of "The Arduino World Book" code_Project_78 
- code_Project_75
-  By:Farkad Adnan فرقد عدنان - 
 -E-mail: farkad.hpfa95@gmail.com 
-inst : farkadadnan 
- #farkadadnan , #farkad_adnan , فرقد عدنان# 
- FaceBook: كتاب عالم الاردوينو 
- inst : arduinobook
1. #كتاب_عالم_الاردوينو
2. #كتاب_عالم_الآردوينو

* facebook : https://www.facebook.com/profile.php?id=100002145048612-
* instagram:  https://www.instagram.com/farkadadnan/
* linkedin : https://www.linkedin.com/in/farkad-adnan-499972121/

 <p>
 <a href='https://mobile.twitter.com/farkadadnan'>
        <img alt="Twitter Follow" src="https://img.shields.io/twitter/follow/farkadadnan?label=%40farkadadnan&style=social" alt='Twitter' align="center"/>
    </a>
</p>

# SKU-SEN0291-Gravity-I2C-Digital-Wattmeter-SEN0291

![111](https://user-images.githubusercontent.com/35774039/161133526-69ffb207-44cb-4ab9-8d2c-855125933ec4.JPG)

# Introduction
- ان دارة I2C Digital Wattmeter عبارة عن لوحة  قياس يمكنها قياس الجهد والتيار والطاقة لمختلف الوحات الإلكترونية والمعدات الكهربائية في حدود V26 و A8 ، والحد الأقصى للخطأ النسبي لا يزيد عن ± 0.2٪. يمكن استخدامه لاستهلاك الطاقة أو تقييم عمر البطارية لأنظمة الطاقة الشمسية أو البطارية أو المحركات أو لوحات التحكم .
- The I2C Digital Wattmeter circuit is a measuring panel that can measure the voltage, current and power of various electronic boards and electrical equipment within the limits of V26 and A8, and the maximum relative error is no more than ±0.2%. It can be used for power consumption or battery life assessment of solar energy systems, battery, motors or control panels.

# Features
- High precision, high resolution, large range, low temperature drift
- Bidirectional current high side measurement
- Compatible with 3.3V/5V controller
- Sophisticated and compact, easy to embed in the project

# Application
- Solar Power Management
- Battery Fuel Gauge
- Electronic Module Power Evaluation

# Specification
- Input Voltage (VCC) : 3.3V~5.5V
- Voltage Range (IN+ or IN- relative to GND): 0 ~ 26 V
- Voltage Resolution: 4 mV
- Voltage Relative Error: <±0.2% (Typical)
-Current Range: 0 ~ ±8A (Bidirectional current)
- Current Resolution: 1mA
- Current Relative Error: <±0.2% (Typical, manual calibration required)
- Power Range: 0 ~ 206 W
- Power Resolution: 20 mW (Hardware) / 4 mW (Software)
- Quiescent Current: 0.7 mA
- Interface: Gravity I2C (logic level: 0-VCC)
- I2C Address: Four options 0x40, 0x41, 0x44, 0x45
- Dimension: 30.0mm*22.0mm
- Weight: 4g
- Board Ov

# Board Overview
![SEN0291_overview](https://user-images.githubusercontent.com/35774039/161134376-15571ad7-b744-4b15-b04c-cd32453749ea.png)

![414](https://user-images.githubusercontent.com/35774039/161134385-1eb60a3b-c24a-48ab-af4a-c53dbc6a2d8d.JPG)

ُ# Code Arduino
```
/*
 By:Farkad Adnan
 E-mail: farkad.hpfa95@gmail.com
 inst : farkadadnan
 #farkadadnan , #farkad_adnan , فرقد عدنان#
 FaceBook: كتاب عالم الاردوينو
 inst : arduinobook
 #كتاب_عالم_الاردوينو  #كتاب_عالم_الآردوينو 
 */
#include <Wire.h>
#include "DFRobot_INA219.h"
DFRobot_INA219_IIC     ina219(&Wire, INA219_I2C_ADDRESS4);
float ina219Reading_mA = 1000;
float extMeterReading_mA = 1000;

void setup(void) {
    Serial.begin(115200);
    while(!Serial);

    Serial.println();
    while(ina219.begin() != true) {
        Serial.println("INA219 begin faild");
        delay(2000);
    }
    ina219.linearCalibrate(ina219Reading_mA, extMeterReading_mA);
    Serial.println();
}
void loop(void){
    Serial.print("BusVoltage:   ");
    Serial.print(ina219.getBusVoltage_V(), 2);
    Serial.println("V");
    Serial.print("ShuntVoltage: ");
    Serial.print(ina219.getShuntVoltage_mV(), 3);
    Serial.println("mV");
    Serial.print("Current:      ");
    Serial.print(ina219.getCurrent_mA(), 1);
    Serial.println("mA");
    Serial.print("Power:        ");
    Serial.print(ina219.getPower_mW(), 1);
    Serial.println("mW");
    Serial.println("");
    delay(1000);
}
```
# Results
1. The module prints four parameters every 1s:
   - ShuntVoltage: Voltage of the sampling resistor, IN+ to NI-.
   - BusVoltage: Voltage of IN- to GND.
   - Current: Current flows across IN+ and IN-. If the current flows from IN+ to IN-, the reading is positive. If the current flows from IN- to IN+, the reading is negative.
   - Power: The product of "BusVoltage" and "Current", that is, power. The power resolution read directly from the module is 20mW (hardware mode). If the power is obtained by using the statement "Power = BusVoltage*Current;", the resolution can be increased to 4mW (software mode).

![SEN0291_Arduino_result](https://user-images.githubusercontent.com/35774039/161135501-8bad47bf-8cb9-48b5-a224-0b0e07a4c95f.png)

