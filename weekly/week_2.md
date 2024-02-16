# Project Progress Report - Week 2

## Project Overview

This week I reviewed the "Pico LTE Micropython SDK" codes. I worked to understand the general code structure and the functions of the apps in the code. Apart from these, I installed the `MicroPython` and the `Pico LTE MicroPython SDK` on Raspberry Pi Pico. However, although I tried various ways, I could only register the device to the network once. My problem of not being able to perform network registration continues.

```
# Not registered, but MT is currently trying to attach the network or searching an operator to register

+CREG: 0, 2
```

## Pico LTE Micropython SDK

I will give information about the important files and these files that I think form the main structure of this project.

### [core.py](https://github.com/sixfab/pico_lte_micropython-sdk/blob/master/pico_lte/core.py)

I can say that the main file of the project is the [core.py](https://github.com/sixfab/pico_lte_micropython-sdk/blob/master/pico_lte/core.py) file. This file is where various modules and apps in the project are called in the `PicoLTE` class and their instances are created. I can define the modules and apps called here as the class to which the user must access since the user accesses from this class.

### [manager.py](https://github.com/sixfab/pico_lte_micropython-sdk/blob/master/pico_lte/utils/manager.py)

The [manager.py](https://github.com/sixfab/pico_lte_micropython-sdk/blob/master/pico_lte/utils/manager.py) file, which is at least as important as the [core.py](https://github.com/sixfab/pico_lte_micropython-sdk/blob/master/pico_lte/core.py) file, contains two classes: `Step` and `StateManager`.

`Step` is the class in which each of the steps required to realize the functions in apps and modules is created as an instance. It takes very important values as parameters: the function, the name of the function, the name of the next step if the function is successful, the name of the next step if the function fails, whether the step is the last step or not, etc.

`StateManager` is the class in which the steps I mentioned above are organized to perform various functions in applications and modules. It includes functions such as adding and updating steps, transitions between steps, and returning the answer as a result of the last step.

- ### [network.py](https://github.com/sixfab/pico_lte_micropython-sdk/blob/master/pico_lte/utils/network.py)

It is a file that contains various functions for the device to register to the network.

- ### [atcom.py](https://github.com/sixfab/pico_lte_micropython-sdk/blob/master/pico_lte/utils/atcom.py)

This file, which contains the `ATCom` class, is the file that provides serial port communication. Sending commands to the modem and receiving responses are performed in this class.

- ### ["modules"](https://github.com/sixfab/pico_lte_micropython-sdk/tree/master/pico_lte/modules) folder

Thanks to the functions in this file, logging required for debugging can be enabled or disabled.

- ### ["modules"](https://github.com/sixfab/pico_lte_micropython-sdk/tree/master/pico_lte/modules) folder

This folder contains modules such as `auth`, `file`, `http`, and `mqtt`, where the mentioned modules and their functions are placed.

- ### ["apps"](https://github.com/sixfab/pico_lte_micropython-sdk/tree/master/pico_lte/apps) folder

This folder contains apps such as `aws`, `azure`, `slack`, and `telegram`, where the mentioned apps and their various functions are placed.

## References

1. [Pico LTE MicroPython SDK](https://github.com/sixfab/pico_lte_micropython-sdk)

2. [Sixfab Pico LTE](https://docs.sixfab.com/docs/sixfab-pico-lte-introduction)

## Conclusion

In conclusion, my review of the "Pico LTE MicroPython SDK" codes provided valuable insights into the overall code structure and the functionalities of the included applications. Despite diligent efforts, the challenge of consistently registering the device to the network persisted.
