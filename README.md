# codebits

#### f1-sound-vis.js
This p5.js script visualizes sound levels from a microphone by moving a racecar across a track on the screen. The movement and speed of the car represent the volume level sensed by the mic. Key functionalities include:

- **Initialization**:
  ```javascript
  let mic;
  let vol;
  let startXPos = 5;
  let minSpeed = 0;
  ```
  Defines variables for the microphone input, volume level, and initial positions.

- **Setup Function**:
  ```javascript
  function setup() {
  createCanvas(600, 400);
  mic = new p5.AudioIn();
  mic.start();
  }
  ```
  Sets up the canvas and initializes the audio input (microphone).

- **Sound Level Conversion**:
  ```javascript
  let micLevel = mic.getLevel();
  let speed = round(micLevel * 372.5, 1);
  ```
  The microphone level (`micLevel`) is obtained and converted to a speed value (`speed`). The speed is calculated by multiplying the mic level by 372.5, which is likely a scaling factor.

- **Drawing Car and Background**:
  ```javascript
  drawBackground();
  drawCar(startXPos, 180);
  ```
  Calls `drawBackground()` to draw the track and `drawCar()` to draw the car at a specific position (`startXPos`, 180).

- **Updating Car Position**:
  ```javascript
  startXPos = startXPos + micLevel * 30;
  ```
  The x-position of the car (`startXPos`) is updated based on the microphone level, moving the car across the screen.

- **Displaying Maximum Speed**:
  ```javascript
  if (speed > minSpeed) {
      fill('orange');
      text('MAX SPEED: ' + speed + ' KPH', 80, 320);
      minSpeed = speed;
  } else {
      fill('orange');
      text('MAX SPEED: ' + minSpeed + ' KPH', 80, 320);
  }
  ```
  The maximum speed achieved is displayed on the screen. If the current speed exceeds the previous maximum, it updates the maximum speed.

- **Displaying Current Speed**:
  ```javascript
  fill('orange');
  text('CURR. SPEED: ' + speed + ' KPH', 80, 345);
  ```
  The current speed is displayed on the screen, providing a real-time update of the car's speed.

- **Resetting Car Position**:
  ```javascript
  if (startXPos > 600) {
      startXPos = 0;
  }
  ```
  Resets the car's position to the start of the track once it moves off the canvas.