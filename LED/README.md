# LED
<a href="./image/LED.jpg" target="_blank"><img src="./image/LED.jpg" width="300"></a>

[Webduino 官方教學範例 - LED 燈](https://webduino.io/tutorials/tutorial-01-led.html)

## [燈泡圖片亮 & LED 燈亮](./LED_bright.html)
- GND (接地)：LED 短腳
- 13：LED 長腳

實際接線照片：

<a href="./image/LED_bright.jpg" target="_blank"><img src="./image/LED_bright.jpg" width="300"></a>

```javascript
var led;

boardReady({device: 'wa8w'}, board => {
    board.systemReset();
    board.samplingInterval = 250;
    led = getLed(board, 13);
    led.on();
    document.getElementById("light").className = "on";
});
```

## [點擊燈泡圖片切換 LED 燈開關](./Switch_LED.html)
- GND (接地)：LED 短腳
- 13：LED 長腳

```javascript
var led;
var light = document.getElementById("light");

boardReady({device: 'wa8w'}, board => {
    board.systemReset();
    board.samplingInterval = 250;
    led = getLed(board, 13);
    led.off();
    light.className = "off";
    light.addEventListener("click", () => {
        led.toggle();
        light.className = light.className == "on" ? "off" : "on";
    });
});
```

## 黃亮紅不亮，黃不亮紅亮 切換
- GND (接地)：LED 短腳
- 10：紅 LED 長腳
- 11：黃 LED 長腳

實際接線照片：

<a href="./image/Click_Switch_Yellow-Red_LED_1.jpg" target="_blank"><img src="./image/Click_Switch_Yellow-Red_LED_1.jpg" width="300"></a>

### [點擊燈泡圖片 切換](./Click_Switch_Yellow-Red_LED.html)
```javascript
var led_red, led_yellow;
var light = document.getElementById("light");

boardReady({device: 'wa8w'}, board => {
    board.systemReset();
    board.samplingInterval = 250;
    led_red = getLed(board, 10);
    led_yellow = getLed(board, 11);
    led_red.off();
    led_yellow.on();
    light.className = "off";
    light.addEventListener("click", () => {
        led_red.toggle();
        led_yellow.toggle();
        light.className = light.className == "on" ? "off" : "on";
    });
});
```

### [自動間隔幾秒後 切換](Auto_Switch_Yellow-Red_LED.html)
```javascript
var led_red, led_yellow;
var light = document.getElementById("light");

boardReady({device: 'wa8w'}, board => {
    board.systemReset();
    board.samplingInterval = 250;
    led_red = getLed(board, 10);
    led_yellow = getLed(board, 11);
    led_red.off();
    led_yellow.on();
    light.className = "off";
    setInterval(() => {
        led_red.toggle();
        led_yellow.toggle();
        light.className = light.className == "on" ? "off" : "on";
    }, 2000);
});
```

### Demo

<a href="./image/Click_Switch_Yellow-Red_LED_2.gif" target="_blank"><img src="./image/Click_Switch_Yellow-Red_LED_2.gif" width="300"></a>

## [紅綠燈](./Traffic-light.html)

- GND (接地)：LED 短腳
- 10：紅 LED 長腳
- 11：黃 LED 長腳
- 7：綠 LED 長腳

實際接線照片：

<a href="./image/Auto_Switch_Yellow-Red_LED_1.jpg" target="_blank"><img src="./image/Auto_Switch_Yellow-Red_LED_1.jpg" width="49%"></a>
<a href="./image/Auto_Switch_Yellow-Red_LED_2.jpg" target="_blank"><img src="./image/Auto_Switch_Yellow-Red_LED_2.jpg" width="49%"></a>

說明：
- 開始綠燈亮，可按 點擊燈泡圖片 切換 紅燈 或 綠燈 狀態
- 切換紅燈狀態：點擊燈泡圖片 2 秒後換黃燈亮 (其他不亮)，再 2 秒後換紅燈亮 (其他不亮)
- 切換綠燈狀態：點擊燈泡圖片 2 秒後換綠燈亮 (其他不亮)

```javascript
(async function () {
    var led_red, led_yellow, led_green;
    var light = document.getElementById("light");

    boardReady({device: 'wa8w'}, async board => {
        board.systemReset();
        board.samplingInterval = 250;
        led_red = getLed(board, 10);
        led_yellow = getLed(board, 11);
        led_green = getLed(board, 7);
        led_red.off();
        led_yellow.off();
        led_green.on();
        light.className = "off";
        light.addEventListener("click", async () => {
            if (light.className == "off") {
                await delay(2);
                led_red.off();
                led_yellow.on();
                led_green.off();
                await delay(2);
                led_red.on();
                led_yellow.off();
                led_green.off();
                light.className = light.className == "on" ? "off" : "on";
            } else {
                await delay(2);
                led_red.off();
                led_yellow.off();
                led_green.on();
                light.className = light.className == "on" ? "off" : "on";
            }
        });
    });
}());
```

### Demo
<a href="./image/Auto_Switch_Yellow-Red_LED_3.jpg" target="_blank"><img src="./image/Auto_Switch_Yellow-Red_LED_3.jpg" width="49%"></a>