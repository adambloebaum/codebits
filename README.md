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

#### citation_transaction.js
This script is used for issuing new parking citations in the parking management system.

- **Starting Transaction**:
  ```javascript
  DBManager.beginTransaction();
  ```
  Begins a database transaction to ensure data consistency during the citation issuing process.

- **Citation Number Input**:
  ```javascript
  int cNumber = Input.getInt("Enter citation number: ");
  if (cNumber < 0 || cNumber > 999999999) {
      System.out.println("Invalid citation number. It should be 1 to 9 digits.");
  }
  ```
  Prompts for and validates the citation number, ensuring it is within a valid range.

- **Date Input**:
  ```javascript
  String date = Input.getString("Enter date (YYYY-MM-DD): ");
  ```
  Collects the date of the citation, validating the format.

#### permit_transaction.js
This script facilitates the assignment of new parking permits.

- **Starting Transaction**:
  ```javascript
  DBManager.beginTransaction();
  ```
  Initiates a database transaction for assigning a parking permit.

- **Permit ID Input**:
  ```javascript
  int permitID = Input.getInt("Enter permit ID: ");
  if (permitID < 0 || permitID > 999999999) {
      System.out.println("Invalid Permit ID. It should be 1 to 9 digits.");
      return false;
  }
  ```
  Requests and validates the permit ID.

- **Permit Type Input**:
  ```javascript
  String permitType = Input.getString("Enter permit type: ");
  ```
  Gathers the type of permit being assigned, ensuring it's a valid input.

Here are the descriptions for the `citation_transaction.sql` and `parking_transaction.sql` scripts, along with relevant code snippets in Markdown format:

#### citation_transaction.sql
This SQL script is used for processing parking citations in a parking management system.

- **Beginning Transaction**:
  ```sql
  BEGIN TRANSACTION;
  ```
  Initiates a database transaction to ensure data consistency.

- **Variable Declarations**:
  ```sql
  DECLARE @CNumber INT = [your_citation_number];
  DECLARE @Date DATE = GETDATE();
  DECLARE @Fee DECIMAL(10, 2) = [fee_amount];
  DECLARE @Category VARCHAR(20) = '[category]';
  ...
  ```
  Declares variables to store citation details like citation number, date, fee, category, and others.

- **Transaction Handling**:
  ```sql
  COMMIT;
  ```
  Commits the transaction to save the changes, or `ROLLBACK` in case of errors.

#### parking_transaction.sql
This script handles the assignment of parking permits.

- **Beginning Transaction**:
  ```sql
  BEGIN TRANSACTION;
  ```
  Starts a database transaction for permit assignment.

- **Variable Declarations**:
  ```sql
  DECLARE @PermitID INT = [your_permit_id];
  DECLARE @PermitType VARCHAR(50) = '[permit_type]';
  DECLARE @StartDate DATE = '[start_date]';
  DECLARE @ExpDate DATE = '[exp_date]';
  DECLARE @ExpTime TIME = '[exp_time]';
  ...
  ```
  Sets up variables for permit details like permit ID, type, start date, expiration date, etc.

- **Transaction Handling**:
  ```sql
  COMMIT;
  ```
  Commits the transaction to save the changes, or `ROLLBACK` in case of errors.