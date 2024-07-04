#include <OLED_I2C.h>

OLED  oled(SDA, SCL, 8);

extern uint8_t SmallFont[];
extern uint8_t MediumNumbers[];
extern uint8_t BigNumbers[];

const int OUT_PIN = A2;
const int IN_PIN = A0;
float acumulado=0;
float actualizado=0;

void setup(){
   Serial.begin(9600);
   pinMode(OUT_PIN, OUTPUT);
   pinMode(IN_PIN, OUTPUT);
   oled.begin();
   oled.setFont(SmallFont);
   oled.print("PICO CAPACIMETRO", CENTER, 0);
   oled.update();
   delay(1500);
   oled.clrScr();
}
void loop(){
  oled.setFont(SmallFont);
   for(int i=0; i<100; i++){
      pinMode(IN_PIN, INPUT);
      digitalWrite(OUT_PIN, HIGH);
      int val = analogRead(IN_PIN);
      digitalWrite(OUT_PIN, LOW);
      pinMode(IN_PIN, OUTPUT);
      float capacitancia = (float)val * 24 / (float)(1023 - val) ;
      acumulado = capacitancia + acumulado;
    }

   actualizado = acumulado/100;
   acumulado=0;
   Serial.print("Valor en pF:");
   Serial.println(actualizado);
   oled.print("Capacidad[pf]:  ", CENTER, 0);
   oled.setFont(BigNumbers);
   oled.print(String(actualizado), CENTER, 18);
   oled.update();
   delay(1000);
   oled.clrScr();
   delay(100);
}
