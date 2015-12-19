/*
  Serial Event example
 When new serial data arrives, this sketch adds it to a String.
 When a newline is received, the loop prints the string and
 clears it.
 A good test for this is to try it with a GPS receiver
 that sends out NMEA 0183 sentences.
 Created 9 May 2011
 by Tom Igoe
 This example code is in the public domain.
 http://www.arduino.cc/en/Tutorial/SerialEvent
 */
#include "pitches.h"
int buzzer = 9;
const int threshold = 10;    // minimum reading of the sensors that generates a note

//                     *************SONG NOTES & TEMPO***********
int Guile_themeMusic[] = {
  
NOTE_DS4,NOTE_DS4,NOTE_D4,0,NOTE_D4,NOTE_DS4,NOTE_D4,// 1th measure
NOTE_DS4,NOTE_DS4,NOTE_D4,0,NOTE_D4,NOTE_DS4,NOTE_D4, // 2TH measure
NOTE_DS4,NOTE_D4,NOTE_DS4,0,NOTE_D4,NOTE_F4,0,NOTE_F4,NOTE_DS4,NOTE_D4,NOTE_AS3, // 3 MEASURE 25

NOTE_DS4,NOTE_DS4,NOTE_D4,0,NOTE_D4,NOTE_DS4,NOTE_D4,// 4 MEASURE
NOTE_DS4,NOTE_DS4,NOTE_D4,0,NOTE_D4,NOTE_DS4,NOTE_D4, // 5 MEASURE
NOTE_DS4,NOTE_D4,NOTE_DS4,0,NOTE_D4,NOTE_F4,0,NOTE_F4,NOTE_DS4,NOTE_D4,NOTE_AS3, //6 MEASURE 50

NOTE_C3,NOTE_D3,NOTE_DS3,NOTE_F3, // 7 MEASURE
NOTE_G3,NOTE_G3,NOTE_F3,NOTE_AS3,NOTE_GS3,NOTE_G3,NOTE_GS3, //8 MEASURE
NOTE_D3,NOTE_DS3,NOTE_F3,0,NOTE_AS3,NOTE_D3,NOTE_F3, // 9 MEASURE
NOTE_GS3,NOTE_AS3,NOTE_G3,0,NOTE_G3,NOTE_F3,NOTE_D3, // 10 MEASURE  75

NOTE_C3,NOTE_D3,NOTE_DS3,NOTE_F3, //11 MEASURE
NOTE_G3,NOTE_G3,NOTE_GS3,NOTE_F3,0,NOTE_F3,NOTE_G3,NOTE_GS3, //12 MEASURE
NOTE_AS3,NOTE_C4,NOTE_D4,NOTE_DS4,// 13 MEASURE
NOTE_G4,NOTE_F4,NOTE_D4,NOTE_AS3,// 14 MEASURE
NOTE_C4,NOTE_D4,NOTE_DS4,NOTE_F4, // 15MEASURE  //99

NOTE_C4,NOTE_D4,NOTE_DS4,NOTE_F4, // 16 MEASURE
NOTE_G4,NOTE_C4,NOTE_C4,//17TH + 18TH MEASURE
NOTE_GS4,NOTE_G4,NOTE_F4,NOTE_G4, //19 MEASURE
NOTE_F4,NOTE_DS4,NOTE_D4,NOTE_AS3,// 20 MEASURE

NOTE_C4, NOTE_G3, NOTE_AS3,NOTE_AS3,  // 21+22 MEASURE
NOTE_C4, NOTE_D4, NOTE_DS4,NOTE_F4,NOTE_G4,NOTE_GS4,NOTE_F4,0,NOTE_D4,NOTE_D4,//23+24 MEASURE
NOTE_D4, NOTE_DS4,NOTE_F4,0,NOTE_AS3,NOTE_DS4,NOTE_GS4,NOTE_G4,NOTE_F4,NOTE_G4,NOTE_F4,NOTE_DS4,//25+26 measure
NOTE_C4, NOTE_D4, NOTE_DS4, NOTE_F4, //27 MEASURE 
NOTE_F4, NOTE_G4, NOTE_DS4, NOTE_D4,//28 MEASURE
NOTE_D4, NOTE_DS4,NOTE_C4,NOTE_AS3,NOTE_AS3, // 29 + 30 MEASURE
NOTE_C4,0,NOTE_D4,NOTE_DS4,NOTE_F4,NOTE_G4,NOTE_C4,NOTE_AS5,NOTE_GS4,NOTE_G4,NOTE_F4,// 31 +32 MEASURE
NOTE_D4,NOTE_DS4,NOTE_C4// 33+34 MEASURE
};
float Guile_tempo[] = {
  8,16,16,16,16,2,8, //measure 1
8,16,16,16,16,2,8,
16,8,16,16,8,16,16,16,8,8,8,

8,16,16,16,16,2,8, //measure 4
8,16,16,16,16,2,8,
16,8,16,16,8,16,16,16,8,8,8,

1.6,8,16,5.3,  //measure 7
5.3,16,8,4,8,16,5.3,
5.3,5.3,8,8,8,8,8,
5.3,5.3,8,8,8,8,8,

1.6,8,16,5.3, //measure 11
5.3,16,8,8,8,8,16,5.3,
1.6,8,16,5.3,
4,4,4,4,
1.6,8,8,8,

1.6,8,8,8,  //measure 16
0.5714,8,8,  //2 measures in one line
1.6,8,16,5.3,
4,4,4,4,
4,0.6667,8,8,
1.6,8,16,8,4,5.3,8,8,8,16,5.3,
4,5.3,16,5.3,8,8,4,16,16,4,8,8,

1.6,8,8,8,// measure 27
1.6,8,16,5.3,
8,16,0.64,8,8,
2,8,8,16,8,3.2,5.3,5.3,8,8,8,
8,16,0.5517

};
int mortalkombattheme[] = {
  NOTE_A3, NOTE_A3, NOTE_C4, NOTE_A3, NOTE_D4, NOTE_A3, NOTE_E4, NOTE_D4, //A 1th measure
  NOTE_C4, NOTE_C4, NOTE_E4, NOTE_C4, NOTE_G4, NOTE_C4, NOTE_E4, NOTE_C4, // 2th measure
  NOTE_G3, NOTE_G3, NOTE_B3, NOTE_G3, NOTE_C4, NOTE_G3, NOTE_D4, NOTE_C4, // 3th measure
  NOTE_F3, NOTE_F3, NOTE_A3, NOTE_F3, NOTE_C4, NOTE_F3, NOTE_C4, NOTE_B3, //4th measure

  NOTE_A3, NOTE_A3, NOTE_A3, NOTE_A3, NOTE_G3, NOTE_C4, //B 5,measure
  NOTE_A3, NOTE_A3, NOTE_A3, NOTE_A3, NOTE_G3, NOTE_E3, // 6th measure
  NOTE_A3, NOTE_A3, NOTE_A3, NOTE_A3, NOTE_G3, NOTE_C4, // 7th measure
  NOTE_A3, NOTE_A3, NOTE_A3, NOTE_A3, NOTE_A3, NOTE_A3, NOTE_A3, 0, // 8th measure
  //C
  NOTE_A3, NOTE_E4, NOTE_A3, NOTE_C4, NOTE_A3, NOTE_AS3, NOTE_A3, NOTE_C4, NOTE_A3, NOTE_AS3, NOTE_G3, //9th measure
  NOTE_A3, NOTE_E4, NOTE_A3, NOTE_C4, NOTE_A3, NOTE_AS3, NOTE_A3, NOTE_C4, NOTE_A3, NOTE_AS3, NOTE_G3, //10th measure
  NOTE_A3, NOTE_E4, NOTE_A3, NOTE_C4, NOTE_A3, NOTE_AS3, NOTE_A3, NOTE_C4, NOTE_A3, NOTE_AS3, NOTE_G3, // 11th measure
  NOTE_A3, NOTE_E4, NOTE_A3, NOTE_C4, NOTE_A3, NOTE_G3, NOTE_G3, NOTE_A3, //12th measure

  NOTE_A3, NOTE_A3, NOTE_A3, NOTE_A3, NOTE_G3, NOTE_C4, // D 13th measure
  NOTE_A3, NOTE_A3, NOTE_A3, NOTE_A3, NOTE_G3, NOTE_E3, // 14th measure
  NOTE_A3, NOTE_A3, NOTE_A3, NOTE_A3, NOTE_G3, NOTE_C4, // 15th measure
  NOTE_A3, NOTE_A3, NOTE_A3, NOTE_A3, NOTE_A3, NOTE_A3, NOTE_A3, 0, //16th measure

  NOTE_A3, NOTE_A3, NOTE_C4, NOTE_A3, NOTE_D4, NOTE_A3, NOTE_E4, NOTE_D4, //E 17measure
  NOTE_C4, NOTE_C4, NOTE_E4, NOTE_C4, NOTE_G4, NOTE_C4, NOTE_E4, NOTE_C4, // 18th measure
  NOTE_G3, NOTE_G3, NOTE_B3, NOTE_G3, NOTE_C4, NOTE_G3, NOTE_D4, NOTE_C4, // 19th measure
  NOTE_F3, NOTE_F3, NOTE_A3, NOTE_F3, NOTE_C4, NOTE_F3, NOTE_C4, NOTE_B3 // 20th measure
};

int mortalkombattheme_tempo[] = {
  8, 8, 8, 8, 8, 8, 8, 8, //A
  8, 8, 8, 8, 8, 8, 8, 8,
  8, 8, 8, 8, 8, 8, 8, 8,
  8, 8, 8, 8, 8, 8, 8, 8, 

  5.3, 5.3, 5.3, 5.3, 8, 8, //B
  5.3, 5.3, 5.3, 5.3, 8, 8,
  5.3, 5.3, 5.3, 5.3, 8, 8,
  5.3, 5.3, 8, 8, 8, 8, 8, 8, 

  16, 8, 16, 8, 16, 8, 16, 8, 16, 16, 8, //C
  16, 8, 16, 8, 16, 8, 16, 8, 16, 16, 8,
  16, 8, 16, 8, 16, 8, 16, 8, 16, 16, 8,
  16, 8, 16, 8, 8, 8, 8, 4, 


  5.3, 5.3, 5.3, 5.3, 8, 8, //D
  5.3, 5.3, 5.3, 5.3, 8, 8,
  5.3, 5.3, 5.3, 5.3, 8, 8,
  5.3, 5.3, 8, 12, 12, 12, 8, 8,

  8, 8, 8, 8, 8, 8, 8, 8, //E
  8, 8, 8, 8, 8, 8, 8, 8,
  8, 8, 8, 8, 8, 8, 8, 8,
  8, 8, 8, 8, 8, 8, 8, 8
};



String inputString = "";         // a string to hold incoming data
boolean stringComplete = false;  // whether the string is complete
int state=0;
void setup() {
  // initialize serial:
  Serial.begin(9600);
  // reserve 200 bytes for the inputString:
  inputString.reserve(200);  
}


//                  ********************MAIN******************
void loop() {
  serialEvent(); //call the function
  // print the string when a newline arrives:
  if (stringComplete) {
    inputString.trim();
    Serial.println(inputString);
    
    if(inputString.equals("1")){
      state=1;
    }
    else if(inputString.equals("2")){
      state=2;
    }
    else if(inputString.equals("3")){
      state=0;
    }

    
    // clear the string:
    inputString = "";
    stringComplete = false;
    Serial.println("OK");
    
  }

  //running(playing) the songs
  if (state==0)
  {
    //No songs played
  }
  else if (state==1)
  {
    sing1();
  }
  else if (state==2)
  {
    sing2();
  }
}

//                         **************METHODS*************
//                           ***********SONG LIST***********
void sing1()
{
  //int len = sizeof(underworld_melody);
  for (int i = 0; i < 166; i++)
  {
    float noteDuration = 1000 / Guile_tempo[i];
    tone(buzzer, Guile_themeMusic[i], noteDuration);
    float pauseBetweenNotes = noteDuration * 1.30;
    /*Serial.print(i);
    Serial.print(" + ");
    Serial.println(Guile_tempo[i]);*/
    delay(pauseBetweenNotes);
    
    serialEvent();
    if (stringComplete)
    {
      break;
    }
    tone(buzzer, 0, noteDuration); //stop the tone playing
  }
}
void sing2()
{
  
  for (int i = 0; i < 157; i++)
  {
    int noteDuration = 1000 / mortalkombattheme_tempo[i];

    tone(buzzer, mortalkombattheme[i], noteDuration);

    int pauseBetweenNotes = noteDuration * 1.30;
    delay(pauseBetweenNotes);
    
    serialEvent();
    if (stringComplete)
    {
      break;
    }
    tone(buzzer, 0, noteDuration); //stop the tone playing
  }
}



/*
  SerialEvent occurs whenever a new data comes in the
 hardware serial RX.  This routine is run between each
 time loop() runs, so using delay inside loop can delay
 response.  Multiple bytes of data may be available.
 */
void serialEvent() {
  while (Serial.available()) {
    // get the new byte:
    char inChar = (char)Serial.read();
    // add it to the inputString:
    inputString += inChar;
    // if the incoming character is a newline, set a flag
    // so the main loop can do something about it:
    if (inChar == '\n') {
      stringComplete = true;
    }
  }
}
