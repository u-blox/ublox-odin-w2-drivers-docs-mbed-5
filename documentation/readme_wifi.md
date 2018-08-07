# u-blox Wi-Fi driver
The Wi-Fi driver provides functionality to initialize, configure and manage a Wireless LAN connection using the ODIN-W2 module. A supplicant is included to enable authentication and encryption handling.

The Wi-Fi support conforms to IEEE 802.11a/b/g/n and has dual-band 2.4 GHz and 5GHz operation. The driver can either operate as a Station or an Access Point.

The Wi-Fi driver is typically used together with a TCP/IP stack. For Arm Mbed OS 5 the OdinWiFiInterface class uses the included IP-stack.

The following chapters describes the usage with the C API. For the C++ API see header files and [example](https://github.com/ARMmbed/mbed-os-example-wifi) in mbed-os.

## General initialization
The Wi-Fi driver is initialized with a call to cbMAIN\_initWlan. Note that cbWLAN\_init must not be called since this is done from inside cbMAIN\_initWlan.

In order to get status updates it's necessary to register via the cbWLAN\_registerStatusCallback function.

Once the driver has been initialized and a status handler been registered it can be started with cbMAIN\_startWlan. When starting is finished a status event/callback is received.

If the driver is not intended to be in use any more it is wise to stop it with cbWLAN\_stop to lower power consumption.

For the OdinWiFiInterface class all of the functions above is done in the constructor and destructor.

## Station mode
The station mode is entered by calling any of the cbWLAN\_connectXXX functions. Whenever a connection is dropped the application will be notified and the driver will re-connect until a connection is re-established. The connection can be cancelled or terminated by calling cbWLAN\_disconnect.

Although a scan is not necessary prior to a connection establishment it might be required if full information about the access point is needed.

### 802.11r (over the DS/AIR)
Roaming capability is always turned on while working in station mode. If an access point is 802.11r supported, connection between station and access point will be established using this feature by default. Connections with access points that do not support 802.11r will be established without using this roaming capability.

## Acess Point (Pending release)

The AP mode require macro DEVICE_WIFI_AP to be defined in mbed_app.json . To enter the AP mode by calling ap_start should be called. To stop the AP mode ap_stop needs to be called. 
A public example for AP mode will soon be released. 
