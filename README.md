## dts 配置

```C
#include <dt-bindings/gpio/nca9555-gpio.h>

...

&i2c3 {
    status = "okay";
    pinctrl-names = "default";
    pinctrl-0 = <&i2c3m1_xfer>;
    nca9555: mfd-gpio@20 {
        compatible = "nca9555";
        reg = <0x20>;
        status = "okay";

        nca9555_gpio: gpio-normal@20 {
            compatible = "nca9555-gpio";
            gpio-controller;
            #gpio-cells = <2>;
        };
    };
};
```

## 引用GPIO

```C
vcc5v0_usb: vcc5v0-usb {
	compatible = "regulator-fixed";
	regulator-name = "vcc5v0_usb";
	regulator-min-microvolt = <5000000>;
	regulator-max-microvolt = <5000000>;
	enable-active-high;
	gpio = <&nca9555_gpio IO_00 GPIO_ACTIVE_HIGH>;
};
```
