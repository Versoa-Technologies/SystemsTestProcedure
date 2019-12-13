# SystemsTestProcedure
Test procedure to test intake system

#include <Servo.h>

int ByteReceived;
int pos = 0;
Servo servo1;
Servo servo2;

void setup()
{
  Serial.begin(9600);  
  Serial.println("--- Start Serial Monitor SEND_RCVE ---");
    Serial.println(" Type in Box above, . ");
//  Serial.println("(Decimal)(Hex)(Character)");  
//  Serial.println(); 
  servo1.attach(10);
  servo2.attach(11);
  servo1.write(0);
  servo2.write(180);
}

void loop()
{
  if (Serial.available() > 0)
  {
    ByteReceived = Serial.read();
    
    if(ByteReceived == '1') // Single Quote! This is a character.
    {
      Serial.print("closing");
      for (pos = 0; pos <= 180; pos += 1) { // goes from 180 degrees to 0 degrees
      servo1.write(pos);  // tell servo to go to position in variable 'pos'
      servo2.write(180-pos);
      delay(10);               // waits 10ms for the servo to reach the position, adjust delay in order to open/close faster        
      }
    }
    
    if(ByteReceived == '0')
    {
      Serial.print("opening");
      for (pos = 180; pos >= 0; pos -= 1) { // goes from 180 degrees to 0 degrees
      servo1.write(pos);              // tell servo to go to position in variable 'pos'
      servo2.write(180-pos);
      delay(10);                       // waits 10ms for the servo to reach the position
        }
    
    Serial.println();    // End the line

  }
}
}
