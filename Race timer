#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

const int startButtonPin = 2;
const int ldrPin = A0;

unsigned long startTime = 0;
unsigned long stopTime = 0;
float elapsedTime = 0;
boolean running = false;

const int ldrThreshold = 700;

void setup() {
  lcd.init();
  lcd.backlight();
  pinMode(startButtonPin, INPUT_PULLUP);
}

void loop() {
  if (digitalRead(startButtonPin) == LOW && !running) {
    startTime = millis();
    elapsedTime = 0;
    running = true;
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Running");
  }
  if (analogRead(ldrPin) > ldrThreshold && running) {
    // stop the stopwatch
    stopTime = millis();
    elapsedTime = (stopTime - startTime) / 1000.0;
    running = false;
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Elapsed time:");
    lcd.setCursor(0, 1);
    lcd.print(elapsedTime, 3);
    lcd.print(" sec");
  }
}
