notro/rpi-firmware
==========

Raspberry Pi kernel 3.18.5-v7+ with support for FBTFT.

Install
-------

```text
sudo REPO_URI=https://github.com/notro/rpi-firmware rpi-update
```



Changelog
---------
2015-02-07
* Pi 2 support

2014-12-07
* [fbtft_device: added support for waveshare32b](https://github.com/notro/fbtft/commit/e67014490a9df34b9a4bf04e49c50254aebc10a8)
* [fbtft_device: add Tontec 3.5 support](https://github.com/notro/fbtft/commit/8116d7273be8816ce70c1a017b4466ae17e27d53)
* [fb_ili9481,6: regwidth was incorrect](https://github.com/notro/fbtft/commit/c92097b5a5ef82e298a4fe8ec7859c9378e435d8)
* [fbtft: make it possible to override regwidth](https://github.com/notro/fbtft/commit/566dca0e9d531b54c11ea9aea47f76695472776c)

2014-11-28
* [add support for AGM1264K-FL](https://github.com/notro/fbtft/commit/de1c2adfbb7b04b90a02d0e4cf6d7d923bab3656)
* [uc1701: add support for UC1701](https://github.com/notro/fbtft/commit/43d452d3b2f4ce9193103603bb453d4a97ff11f6)
* [fbtft_device: add adafruit28](https://github.com/notro/fbtft/commit/32995715c7fb161bf539fefc7e250fef3599cd61)
* [add ILI9481 support](https://github.com/notro/fbtft/commit/a693c8e3692f6a4fb67468a2d3b3fdd35b9aa2e2)
* [add support for the TLS8204 used in the latest Nokia 3310 displays](https://github.com/notro/fbtft/commit/6da654310724c31622afa8c7d12211a6e33ec18d)

2014-08-02
* add er_tftm050_2 and er_tftm070_5 support
* add RA8875 support
* add support for PiScreen
* add ILI9486 support
* add S6D02A1 support (Wolfgang Buening)
* rpi_power_switch was missing in the previous release

2014-06-14
* fb_ssd1351: Add rotation support
* Add Waveshare 2.2" (bd663474 & upd161704) support
* install_kernel_source is removed
* rpi-source support added

2014-03-28
* fix stmpe-ts
  Interrupts was missed resulting in driver hang
* add rpi_power_switch module
  Turn on/off the Raspberry Pi with a button

2014-03-08
* fix path in install_kernel_source

2014-03-08
* add extra/{git_hash,install_kernel_source}

2014-03-06
* Add displays rpi-display and pitft
* Add modules 'stmpe' and 'gpio_backlight'
* DMA is enabled by default

2013-12-14
* add tinylcd35 support

2013-12-08
* Moved to Linux version 3.10
* fbtft_device: add hy28b support
* Add support for S6D1121

2013-11-18
* fb_ssd1306: add support for Adafruit OLED 1.3" monochrome display
* fb_ili9340: add support for the new Adafruit 2.2" display
* Enable console rotation support (fbcon=rotate:1)

2013-09-18
* fbtft: fix performance debug output
* flexfb: add 9-bit SPI emulation support
* fb_watterott: add support for mi0283qt-v2
* fbtft: experimental DMA support
* fbtft: turn off backlight before device removal

Thanks to Derek Campbell (guzunty) there is now experimental DMA support for SPI in FBTFT.
The CPU runs much lighter using DMA:  https://github.com/notro/fbtft/wiki/FPS#testing-with-dma-support

2013-09-02
* fbtft_device: Add support for Freetronics OLED128 module and Tianma TM022HDH26
* fb_ssd1351: added chip gpio support (backlight)
* ads7846_device: moved to https://github.com/notro/fbtft_tools
* fbtft: add active low backlight pinname: 'led_'

2013-08-22
* All drivers have been rewritten (except flexfb). They now contain only LCD Controller specific logic and a default init sequence. fbtft_device contains the display specific information.
  Show supported displays like this: sudo modprobe fbtft_device name=list; dmesg | tail -30
* 'rotate' argument is now a conter clockwise angle: 0, 90, 180, 270
* All drivers support all interface modes: SPI 8-bit + D/C, 8-bit + startbyte, 9-bit, GPIO 8, 16 bit (even though the LCD controller might not).
* The drivers will also load automatically when the device is present (need only load fbtft_device).
* The init sequence can be overridden on all drivers with the fbtft_device init argument.



Sources
-------
* [raspberrypi/firmware](https://github.com/raspberrypi/firmware/archive/e42a747e8d5c4a2fb3e837d0924c7cc39999936a.tar.gz)
* [raspberrypi/linux](https://github.com/raspberrypi/linux/archive/a6cf3c99bc89e2c010c2f78fbf9e3ed478ccfd46.tar.gz)
* [notro/spi-bcm2708](https://github.com/notro/spi-bcm2708/archive/57fc2d1ea38e337ea04bd4e05a24cc94eea11a8b.tar.gz)
* [notro/fbtft](https://github.com/notro/fbtft/archive/855b2908380e8ca996768bf94cb4d8573690bc30.tar.gz)
* [notro/fbtft_tools](https://github.com/notro/fbtft_tools/archive/8553a4b1f5262c6dd076bb5fdd3e97ec7e3cdebe.tar.gz)
* [msperl/spi-config](https://github.com/msperl/spi-config/archive/878f592626db291b3a62b5054278c95e92bc0b39.tar.gz)


Patches
--------
* /home/pi/rpi-build/fbtft-build/patches/fbtft.patch/3.15
* /home/pi/rpi-build/fbtft-build/patches/stmpe-ts-Various-fixes.patch/3.10


Kernel config
-------------
Default config: bcmrpi_defconfig



Added:
```text
BACKLIGHT_GPIO=m
CAN=y
CAN_BCM=m
CAN_CALC_BITTIMING=y
CAN_DEV=y
CAN_GW=y
CAN_MCP251X=m
CAN_RAW=m
CAN_SLCAN=m
CAN_VCAN=m
DYNAMIC_DEBUG=y
FB_BACKLIGHT=y
FB_DEFERRED_IO=y
FB_FLEX=m
FB_SYS_COPYAREA=m
FB_SYS_FILLRECT=m
FB_SYS_FOPS=m
FB_SYS_IMAGEBLIT=m
FB_TFT=m
FB_TFT_AGM1264K_FL=m
FB_TFT_BD663474=m
FB_TFT_FBTFT_DEVICE=m
FB_TFT_HX8340BN=m
FB_TFT_HX8347D=m
FB_TFT_HX8353D=m
FB_TFT_ILI9320=m
FB_TFT_ILI9325=m
FB_TFT_ILI9340=m
FB_TFT_ILI9341=m
FB_TFT_ILI9481=m
FB_TFT_ILI9486=m
FB_TFT_PCD8544=m
FB_TFT_RA8875=m
FB_TFT_S6D02A1=m
FB_TFT_S6D1121=m
FB_TFT_SSD1289=m
FB_TFT_SSD1306=m
FB_TFT_SSD1331=m
FB_TFT_SSD1351=m
FB_TFT_ST7735R=m
FB_TFT_TINYLCD=m
FB_TFT_TLS8204=m
FB_TFT_UC1701=m
FB_TFT_UPD161704=m
FB_TFT_WATTEROTT=m
FONTS=y
FONT_10x18=y
FONT_6x10=y
FONT_6x11=y
FONT_7x14=y
FONT_ACORN_8x8=y
FONT_MINI_4x6=y
FONT_PEARL_8x8=y
FONT_SUN12x22=y
FONT_SUN8x16=y
FRAMEBUFFER_CONSOLE_ROTATION=y
GPIOLIB_IRQCHIP=y
GPIO_MCP23S08=m
GPIO_STMPE=y
INPUT_KEYBOARD=y
INPUT_MOUSE=y
KEYBOARD_GPIO=m
MFD_STMPE=y
MOUSE_GPIO=m
SPI_BITBANG=m
SPI_GPIO=m
STMPE_I2C=y
STMPE_SPI=y
TOUCHSCREEN_STMPE=m
```


Changed:
```text
BACKLIGHT_CLASS_DEVICE m -> y
```


<p align="center">Built with <a href="https://github.com/notro/rpi-build/wiki">rpi-build</a></p>
