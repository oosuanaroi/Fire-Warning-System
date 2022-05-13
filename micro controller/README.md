```C++
// C++ code
//
#include <LiquidCrystal.h>
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);
#define temp A1
#define led 13
void setup()
{
  pinMode(10, OUTPUT);
  pinMode(9, OUTPUT);
  pinMode(8, OUTPUT);
  lcd.begin(16, 2);
  pinMode(led, OUTPUT);
  Serial.begin(9600);
  pinMode(temp, INPUT);
  lcd.clear();
  lcd.print("Temperature: ");
}
float pre_temp = 0;
void loop()
{
  int a=analogRead(A0);
  int b=map(a,0,1023,0,255);
  Serial.println(b);
  float temperature = 0;
  temperature = (analogRead(temp) * 0.48828125) - 49.95;
  if(pre_temp != temperature)
  {
    lcd.setCursor(0,1);
    lcd.print("                ");
  }
  lcd.setCursor(0,1);
  lcd.print(temperature);
  lcd.print(" C");
  pre_temp = temperature;
  
  if (temperature >= 45)
  {
   digitalWrite(10, HIGH);
   tone(7, 400, 100);
  }
  else
  {
    digitalWrite(10, LOW);
  }
  if (b >= 37)
  {
    digitalWrite(9, HIGH);
    tone(7, 400, 100);
  }

  else
  {
    digitalWrite(9, LOW);
  }
}

```