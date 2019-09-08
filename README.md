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
- pull GPIO32 to LOW to enable power on ESP32-CAM board (1V2, 2V8).
```c
#define GPIO_OUTPUT_IO_33    33
#define GPIO_OUTPUT_IO_32    32
#define GPIO_OUTPUT_PIN_SEL  ((1ULL<<GPIO_OUTPUT_IO_32) | (1ULL<<GPIO_OUTPUT_IO_33))

void enable_power_on_camera(void){
     gpio_config_t io_conf;
    //disable interrupt
    io_conf.intr_type = GPIO_PIN_INTR_DISABLE;
    //set as output mode
    io_conf.mode = GPIO_MODE_OUTPUT;
    //bit mask of the pins that you want to set,e.g.GPIO18/19
    io_conf.pin_bit_mask = GPIO_OUTPUT_PIN_SEL;
    //disable pull-down mode
    io_conf.pull_down_en = 0;
    //disable pull-up mode
    io_conf.pull_up_en = 0;
    //configure GPIO with the given settings
    gpio_config(&io_conf);

    gpio_set_level(GPIO_OUTPUT_IO_32, 0);
    gpio_set_level(GPIO_OUTPUT_IO_33, 0);
}
```
- Deselect OV3660 support ; Deselect use hardware I2C1 support

`idf.py menuconfig -> Component config -> Camera configuration ->select OV2460 support`

References:
https://github.com/espressif/esp-who/issues/57

## Command Prompt:
- list all file: `dir`
- change disk:  `E:` or `C:`
