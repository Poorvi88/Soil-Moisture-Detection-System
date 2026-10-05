# Soil-Moisture-Detection-System
Smart Monitoring for Healthier soil &amp;Better Crop Selection
/*
  Soil Moisture Monitor + Crop Recommendation (LCD Debug Version)
  - Same logic as before, but with a clear LCD startup test
    so you can immediately confirm the LCD is receiving data.

  IMPORTANT: Before using this, run i2c_scanner.ino once to confirm
  your LCD's real address, then set LCD_ADDRESS below to match.

  Wiring:
  Soil sensor: VCC->5V, GND->GND, AOUT->A0
  I2C LCD:     VCC->5V, GND->GND, SDA->A4, SCL->A5
  Buzzer:      + -> Pin 8, - -> GND
*/  

#include <Wire.h>
#include <LiquidCrystal_I2C.h>

// >>> SET THIS to whatever the I2C scanner found (0x27, 0x3F, etc.) <<<
#define LCD_ADDRESS 0x27

LiquidCrystal_I2C lcd(LCD_ADDRESS, 16, 2);   

const int SENSOR_PIN = A0;
const int BUZZER_PIN = 8;

int DRY_VALUE = 620;
int WET_VALUE = 260;

const int DRY_THRESHOLD = 30;
const int MOIST_THRESHOLD = 70;

unsigned long lastSwitch = 0;
bool showCropScreen = false;
const unsigned long SCREEN_INTERVAL = 3000;

enum SoilStatus { STATUS_DRY, STATUS_MOIST, STATUS_WET };

void setup() {
  Serial.begin(9600);
  Wire.begin();

  lcd.init();
  lcd.backlight();

  // --- STARTUP TEST: if this text never appears on the physical LCD, ---
  // --- the problem is wiring, address, contrast, or power - not code ---
  lcd.setCursor(0, 0);
  lcd.print("LCD TEST OK");
  lcd.setCursor(0, 1);
  lcd.print("If blank: check");
  Serial.println("If the LCD stays blank, adjust the contrast pot on the");
  Serial.println("backpack, or re-check the I2C address using the scanner.");

  pinMode(BUZZER_PIN, OUTPUT);
  digitalWrite(BUZZER_PIN, LOW);

  delay(3000); // hold test message for 3 sec so you can see it
  lcd.clear();
}

void loop() {
  int rawValue = analogRead(SENSOR_PIN);
  int moisturePercent = map(rawValue, DRY_VALUE, WET_VALUE, 0, 100);
  moisturePercent = constrain(moisturePercent, 0, 100);

  SoilStatus status;
  if (moisturePercent < DRY_THRESHOLD) {
    status = STATUS_DRY;
    digitalWrite(BUZZER_PIN, HIGH);
  } else if (moisturePercent < MOIST_THRESHOLD) {
    status = STATUS_MOIST;
    digitalWrite(BUZZER_PIN, LOW);
  } else {
    status = STATUS_WET;
    digitalWrite(BUZZER_PIN, LOW);
  }

  printSerialInfo(rawValue, moisturePercent, status);
  updateLCD(moisturePercent, status);

  delay(500);
}

void printSerialInfo(int rawValue, int moisturePercent, SoilStatus status) {
  Serial.print("Raw: ");
  Serial.print(rawValue);
  Serial.print("  Moisture: ");
  Serial.print(moisturePercent);
  Serial.print("%  Status: ");
  Serial.println(statusName(status));
  Serial.print("Best crops: ");
  Serial.println(getCropList(status));
  Serial.println("------------------------");
}

void updateLCD(int moisturePercent, SoilStatus status) {
  if (millis() - lastSwitch >= SCREEN_INTERVAL) {
    showCropScreen = !showCropScreen;
    lastSwitch = millis();
    lcd.clear();
  }

  if (!showCropScreen) {
    lcd.setCursor(0, 0);
    lcd.print("Moisture: ");
    lcd.print(moisturePercent);
    lcd.print("%");

    lcd.setCursor(0, 1);
    lcd.print("Status: ");
    lcd.print(statusName(status));
  } else {
    lcd.setCursor(0, 0);
    lcd.print("Best Crop:");
    lcd.setCursor(0, 1);
    lcd.print(getShortCrop(status));
  }
}

const char* statusName(SoilStatus status) {
  switch (status) {
    case STATUS_DRY:   return "DRY";
    case STATUS_MOIST: return "MOIST";
    case STATUS_WET:   return "WET";
    default:           return "N/A";
  }
}

const char* getShortCrop(SoilStatus status) {
  switch (status) {
    case STATUS_DRY:   return "Ragi,Jola,Pulse";
    case STATUS_MOIST: return "Maize,Tom,Okra";
    case STATUS_WET:   return "Paddy,Sugarcane";
    default:           return "N/A";
  }
}

const char* getCropList(SoilStatus status) {
  switch (status) {
    case STATUS_DRY:
      return "Ragi (Finger Millet), Jola (Jowar/Sorghum), Pulses";
    case STATUS_MOIST:
      return "Maize, Tomato, Bendi (Okra), Carrot, Watermelon";
    case STATUS_WET:
      return "Paddy (Rice), Sugarcane";
    default:
      return "N/A";
  }
}
