# stm32 study note -- stm32学习笔记

<p>记录一下学习stm32的笔记以及小project<br>
take notes about stm32 learning</p>

<p>在学习阶段我使用了Nucleo f103RB开发板，开发工具使用了STM32CubeIDE，STM32Monitor和STM32CubeMX软件<br>
board and applications</p>

<p>
  Material used:<br>
  <a href="https://www.youtube.com/watch?v=8S78Ih4SaiE" target="_blank">Get Started With STM32 and Nucleo Tutorial</a><br>
  <a href="https://www.youtube.com/watch?v=vKyL43qXPpk" target="_blank">Learn STM32 Microcontroller Programming</a><br>
  <a href="https://www.bilibili.com/video/BV1ZmGQzsE4N/?p=25&share_source=copy_web&vd_source=20ab236611c0e66cdb2042f6a2c6fc2a" target="_blank">7天入门STM32_HAL库版，手把手带写程序，项目实战教学视频 </a><br>
  <a href="https://www.bilibili.com/video/BV1th411z7sn/?p=6&share_source=copy_web&vd_source=20ab236611c0e66cdb2042f6a2c6fc2a" target="_blank">STM32入门教程-2023版 细致讲解 中文字幕</a>
</p>

## 1. build a LED circuit -- 点亮LED电路 --2026.07.24

<p>这是第一个project，还没有用到代码，只是熟悉一下如何接线<br>
first project is to familiar with the hardware and connecting wires</p>
<p>设计电路时需要注意电阻的选择，注意led的额定电压和电流，然后假设一个流过led的电流，计算出将要选择的电阻的阻值。</p>

<div>
<img src="./pic/pro01-01.webp" height="300px" display="block">
<img src="./pic/pro01-02.webp" height="300px" display="block">
</div>

## 2. make the LED flashing -- 闪烁led灯 -- 2026.07.26

<p>这个project将使用代码让led灯闪烁</p>

```c++
HAL_Delay(500);
HAL_GPIO_TogglePin(GPIOA,GPIO_PIN_5);
```

<p>
  the "500" in the delay code means 500ms. this code will block program. which means when doing delay 500ms, cpu cannot do other things. just wait here.
</p>
<p style="text-indent:2em;">
  "GPIOA" means the module where the pin you are using is located.<br>
  when creating the project via cube MX. if the label of the gpio pin is changed (for example: LED_G)<br>
  the toggle function can be changed like:

  ```c++
  HAL_GPIO_TogglePin(LED_G_GPIO_Port, LED_G_Pin);
  ```
</p>

<img src="./pic/IMG_4998 00_00_00-00_00_30.gif" height="300px">

## 3. button toggle led

<p>
using a button to control the led, turn on / turn off. <br>
the circuit of this project will be devided into two parts. <br>
the first part is linked to the button, and then linked to the GPIO pin to detect input. (pin mode: GPIO_Input) <br>
the second part is the leds. there will be 3 leds in this project.
</p>
