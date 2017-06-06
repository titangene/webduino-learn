# LED

## [燈泡亮 & LED 燈亮](./LED_bright.html)
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

## [開關 LED 燈](./Switch_LED.html)
```javascript
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

