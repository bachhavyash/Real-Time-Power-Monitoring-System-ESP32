#define BLYNK_PRINT Serial
#include <WiFi.h>
#include <BlynkSimpleEsp32.h>
#include <LiquidCrystal.h>

char auth[] = "YourAuthToken";
char ssid[] = "YourWiFiName";
char pass[] = "YourWiFiPassword";

// LCD Pins (RS, E, D4, D5, D6, D7)
LiquidCrystal lcd(13, 12, 14, 27, 26, 25);

#define VOLTAGE_PIN 34
#define CURRENT_PIN 35

float voltage = 0.0;
float current = 0.0;
float power = 0.0;
float energy = 0.0;

float voltageOffset = 0;
float currentOffset = 0;

void setup()
{
  Serial.begin(9600);
  lcd.begin(16, 2);

  WiFi.begin(ssid, pass);
  Blynk.begin(auth, ssid, pass);

  lcd.print("Power Monitor");
  delay(2000);
  lcd.clear();
}

void loop()
{
  Blynk.run();

  // Read analog values
  int voltageRaw = analogRead(VOLTAGE_PIN);
  int currentRaw = analogRead(CURRENT_PIN);

  // Convert ADC to actual voltage
  voltage = (voltageRaw - 2048) * (3.3 / 4095.0) * 100;  
  if (voltage < 0) voltage = -voltage;

  // Convert ADC to actual current
  current = (currentRaw - 2048) * (3.3 / 4095.0) * 30;  
  if (current < 0) current = -current;

  // Calculate Power
  power = voltage * current;

  // Calculate Energy (kWh)
  energy = energy + (power / 3600000.0); 

  // Display on LCD
  lcd.setCursor(0, 0);
  lcd.print("V:");
  lcd.print(voltage);
  lcd.print(" I:");
  lcd.print(current);

  lcd.setCursor(0, 1);
  lcd.print("P:");
  lcd.print(power);
  lcd.print("W");

  // Send to Blynk
  Blynk.virtualWrite(V1, voltage);
  Blynk.virtualWrite(V2, current);
  Blynk.virtualWrite(V3, power);
  Blynk.virtualWrite(V4, energy);

  delay(1000);
}

