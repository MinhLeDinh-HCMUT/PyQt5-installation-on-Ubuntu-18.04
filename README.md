# PyQt5 installation from source on Ubuntu 18.04
The device that this script is used is _Nvida Jetson Nano Developer Kit B01_.
## Device Specification
- Jetpack 4.6
- Ubuntu 18.04
- Default Python version: 3.6.8
## Problems
- In a project where I need to use PyQt5 to design a GUI, it seems that commands like ```$ apt-get``` or ```$ pip install``` cannot be used to install PyQt5. After a while of researching, I found out that this method of installation is also not working with many ARM64 architecture devices, such as Nvidia Jetson Nano in my case.
- To overcome this problem, the solution is to build it from source. When I try this new approach, to my surprise, it works perfectly fine :D
- That is the reason why I want to share this method with whoever needs it, hopes that it works well with your device!
## Procedure
- As PyQt5 requires Python 3.7 or later, makes sure that your device meets this requirement. For me, as I also need to works with other librarys that need high Python version, I will use the Python version 3.11.
- With Jetpack 4.6 and Ubuntu 18.04, it is not possible to install Python version 3.8 and above directly, so I will use the virtual enviroment instead. A tutorial on how to install Python with virtual enviroment by Jetson Hacks can be found here: https://www.youtube.com/watch?v=LSdXakt8nZ8
- Keep the packages up-to-date:

  ```$ sudo apt-get update```

  ```$ sudo apt-get upgrade```

- Install the prerequisites:
  
  ```$ sudo apt-get install build-essential python3-dev python3-pip python3-pyqt5.qtsvg python3-pyqt5.qtwebkit```

- Install SIP:

  ```$ pip install PyQt5-sip```

  If installing SIP with PIP does not work for your device, you can install them from source:
  - Download SIP from here: https://riverbankcomputing.com/software/sip/download
  - Run the following command lines to install the downloaded files:

    ```$ python configure.py ```
    
    ```$ make```
    
    ```$ sudo make install```
- Install PyQt5 with source distribution
  - Download PyQt5 source distribution from here: https://pypi.org/project/PyQt5/5.15.0/#files
  - Unzip that folder and access it:

    ```$ cd PyQt5-5.15.0```

  - Run the following command lines to install PyQt5:
    
    ```$ python3 configure.py --qmake /usr/lib/aarch64-linux-gnu/qt5/bin/qmake```
    
    ```$ make```

    ```$ sudo make install```
- Wait for about _15 to 20 minutes_ for the installtion to finish.
- _Voilà!_ PyQt5 is now installed sucessfully on your device!
## Sample code
- You can check if PyQt5 is installed correctly on your device with the following Python program
```
import sys
from PyQt5.QtWidgets import QApplication, QLabel
app = QApplication(sys.argv)
label = QLabel(“Hello world!”)
label.show()
sys.exit(app.exec_())
```
    
    

  
