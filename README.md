# ESP32_CAMERA
# Initial
## Set path
### IDF_PATH
1. edit file <b>idf_cmd_init.bat</b> (comment line 9 to REM set IDF_PATH=%CD%, or set IDF_PATH=...).
2. open Edit Environment Variables and add <b>IDF_PATH</b>.
### Other Paths
https://docs.espressif.com/projects/esp-idf/en/v3.2.2/get-started-cmake/add-idf_path-to-profile.html

## setting software

### Use External RAM
Component config> ESP32-specific> CONFIG_ESP32_SPIRAM_SUPPORT> SPI RAM config

References:
- https://docs.espressif.com/projects/esp-idf/en/latest/api-guides/external-ram.html
- https://docs.espressif.com/projects/esp-idf/en/latest/api-reference/kconfig.html#config-spiram-use

### Define Pin for ESP32 CAM AI-THINKER

```c
//Ai-Thinker CAM board PIN Map
#define CAM_PIN_PWDN 32  //power down is not used
#define CAM_PIN_RESET -1 //software reset will be performed
#define CAM_PIN_XCLK 0
#define CAM_PIN_SIOD 26
#define CAM_PIN_SIOC 27

#define CAM_PIN_D7 35
#define CAM_PIN_D6 34
#define CAM_PIN_D5 39
#define CAM_PIN_D4 36
#define CAM_PIN_D3 21
#define CAM_PIN_D2 19
#define CAM_PIN_D1 18
#define CAM_PIN_D0 5
#define CAM_PIN_VSYNC 25
#define CAM_PIN_HREF 23
#define CAM_PIN_PCLK 22
```

## Build and run:
https://docs.espressif.com/projects/esp-idf/en/latest/get-started/index.html#get-started-start-project

## Fix bugs
1. Detected camera not supported
error like this:
```
E (273) camera: Detected camera not supported.
E (273) camera: Camera probe failed with error 0x20004
E (273) app_camera: Camera init failed with error
```

- Deselect OV3660 support ; Deselect use hardware I2C1 support

`idf.py menuconfig -> Component config -> Camera configuration ->select OV2460 support`

References:
https://github.com/espressif/esp-who/issues/57

2. sccb: SCCB_Write [ff]=01 failed SCCB_Write [12]=80 failed

set `#define CAM_PIN_PWDN   -1` to `#define CAM_PIN_PWDN   32`

## Command Prompt:
- list all file: `dir`
- change disk:  `E:` or `C:`
