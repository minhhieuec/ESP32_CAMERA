# ESP32_CAMERA]
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

## Build and run:
https://docs.espressif.com/projects/esp-idf/en/latest/get-started/index.html#get-started-start-project

## Command Prompt:
- list all file: `dir`
- change disk:  `E:` or `C:`
```c
end
```
