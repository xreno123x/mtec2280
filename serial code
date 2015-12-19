const int leftButton = 2;    
const int rightButton =  3;      
#include <LiquidCrystal.h>
LiquidCrystal lcd(4, 6, 10, 11, 12, 13);
// variables will change:
String inputString = "";
boolean stringComplete = false;

void setup() {
  pinMode(leftButton, INPUT);      
  pinMode(rightButton, INPUT);
  delay(5000);
  lcd.begin(16, 2);
  // Print a message to the LCD.
  lcd.print("hello, world!");
  lcd.clear();
  Serial.begin(9600);
}

void loop() {
  intro();
  if(stage2Jungle()==1)
  {
    goodEnd();    
  }
  else
  {
    badEnd();
  }
  restart();
}
//                             ******STORY******
void intro()
{
  printStr("Hero Advanture");
  printStr2("Part 2: Jungle");
  lcd.clear();
  
  lcd.setCursor(0,0);
  lcd.print("Look At Monitor");
  
  printSerial("You finally exit the cave, you see a huge forest in front of you.");
  printSerial("You are very hungry as you didn't eat for hours, you found a banana tree.");
  printSerial("As you reach for the banana, you heard a really loud sound.");
  printSerial("Wild MONKEY appeared!");
}

int stage2Jungle()
{
  int HP=5;
  int enemyHP=5;

  while(enemyHP>0 && HP>0)
  {
    Serial.println("");
    Serial.print("HP remaining: ");
    Serial.println(HP);
    Serial.print("Enemy HP remaining: ");
    Serial.println(enemyHP);
    Serial.println("");
    delay(500);

    printSerial("1) ATTACK");
    printSerial("2) DEFEND");
    Serial.println("");
    
    int attack=serialInput();
    int battleResult = stage2Scenario(attack);
    if (battleResult==1)
    {
      HP--;
    }
    else if(battleResult==2)
    {
      enemyHP--;
    }
  }
  
  if (HP==0)  {//u died
    printSerial("Hero Wannabe blacked out!");
    return 0;
  }
  else  {
    printSerial("Wild MONKEY fainted!");
    return 1;
  }
}

//0 = nothing happen
//1 = u take damage
//2 = enemy take damage
int stage2Scenario(int attUsed)
{
  int n=random(5);
  delay(500);
  /*Serial.print("random num= ");
  Serial.println(n);*/
  delay(500);
  if (n==0)
  {
    printSerial("Foe MONKEY is loafing around!");
    delay(500);
    if (attUsed==1)
    {
      printSerial("Hero Wannabe used ATTACK!");
      printSerial("Foe MONKEY takes 1 damage.");
      printSerial("It's super effective!");
      Serial.println("");
      return 2;
    }
    else
    {
      printSerial("Hero Wannabe used DEFEND!");
      printSerial("It's not very effective.");
      Serial.println("");
      return 0;
    }
  }
  else if (n==1)
  {    
    printSerial("Foe MONKEY is used COUNTER!");
    if (attUsed==1)
    {
      printSerial("Hero Wannabe used ATTACK!");
      printSerial("You take 1 damage.");
      printSerial("It's super effective!");
      Serial.println("");
      return 1;
    }
    else
    {
      printSerial("Hero Wannabe used Defend!");
      delay(500);
      Serial.print(".");
      delay(500);
      Serial.print(".");
      delay(500);
      Serial.print(".");
      delay(500);
      Serial.print(".");
      delay(500);
      printSerial("It's not very effective.");
      Serial.println("");
      return 0;
    }
  }
  else if (n==2)
  {
    printSerial("Foe MONKEY used THROW A BANANA");
    delay(500);
    if (attUsed==1)
    {
      printSerial("Hero Wannabe looks at the banana with a very hungry eyes.");
      printSerial("Hero Wannabe is distracted!");
      printSerial("It can't move!");
      delay(500);
      printSerial("Hero Wannabe takes 1 damage.");
      printSerial("It's super effective!");
      Serial.println("");
      return 1;
    }
    else
    {
      printSerial("Hero Wannabe used DEFEND!");
      delay(500);
      printSerial("It's not very effective.");
      Serial.println("");
      return 0;
    }
  }
  else if (n==3)
  {    
    printSerial("Foe MONKEY used FART");
    delay(500);
    if (attUsed==1)
    {
      printSerial("Hero Wannabe used THOUSAND YEARS OF PAIN!");
      delay(500);
      printSerial("Foe Monkey takes 1 damage.");
      printSerial("It's super effective!");
      Serial.println("");
      return 2;
    }
    else
    {
      printSerial("Hero Wannabe used DEFEND!");
      printSerial("The gas gets in your nose anyways.");
      delay(500);
      printSerial("Hero Wannabe takes 1 damage.");
      printSerial("It's super effective!");
      Serial.println("");
      return 1;
    }
  }
  else
  {
    if (attUsed==1)
    {
      printSerial("Hero Wannable is tightening its focus!");
      printSerial("Foe MONKEY used HIGH JUMP KICK");
      printSerial("Hero Wannabe takes 1 damage.");
      printSerial("It's super effective!");
      printSerial("Hero Wannabe loses it's focus!");
      Serial.println("");
      return 1;
    }
    else
    {
      printSerial("Foe MONKEY used HIGH JUMP KICK");
      printSerial("Hero Wannabe used DEFEND!");
      printSerial("Foe MONKEY misses and hurts himself.");
      printSerial("Foe Monkey takes 1 damage.");
      printSerial("It's super effective!");
      Serial.println("");
      return 2;
    }
  }
}

void goodEnd()
{
  printSerial("TO BE CONTINUED!");
}
void badEnd()
{
  printSerial("You lost to a monkey in a fight.");
  printSerial("Now you are being used by the monkey as a slave for the rest of your life.");
  printSerial("Bad End 3:");
  printSerial("Worthless Slave");
}
void restart()
{
  printStr("Press any button");
  printStr2("to restart.   ->");
  lcd.clear();
}

//                            ******METHODS******

//1 = left
//2 = right
int buttonInput()
{
  int buttonPressed=-1;
  while (buttonPressed == -1)
  {
    int leftState = digitalRead(leftButton);
    int rightState = digitalRead(rightButton);
    if (leftState==1)
    {
      buttonPressed=1;
    }
    else if(rightState==1)
    {
      buttonPressed=2;
    }
  }
  return buttonPressed;
}

int serialInput()
{
  inputString="";
  //Serial.println(stringComplete); //Testing Purpose
  while(!stringComplete)
  {
    while (Serial.available()) 
    {// get the new byte:
    char inChar = (char)Serial.read();
    // add it to the inputString:
    //inputString += inChar;


    if (inChar != '\n') {
      inputString += inChar;
    }
    //Serial.print(inputString); //Testing Purpose
    // if the incoming character is a newline, set a flag
    // so the main loop can do something about it:
    if (inChar == '\n') {
      stringComplete = true;
      }
    }
  }
  stringComplete=false; 
  //if it's a number
  if (inputString.equals("1"))
  {
    return 1;
  }
  else if(inputString.equals("2"))
  {
    return 2;
  }
  else //If it's a String
  {    // EX: Attack, ATTACK, attack, Defend, DEFEND, defend.
    inputString.toLowerCase();
    if(inputString.equals("attack"))
    {
      return 1;
    }
    else
    {
      return 2;
    }
  }
}

void printStr(String str)
{
  int len=str.length();
  lcd.setCursor(0,0);
  for (int i=0; i<len; i++)
  {
    lcd.print(str.charAt(i));
    //Serial.print(str.charAt(i));
    delay(50);
  }
}
int printStr2(String str)
{
  int len=str.length();
  lcd.setCursor(0,1);
  for (int i=0; i<len; i++)
  {
    lcd.print(str.charAt(i));
    //Serial.print(str.charAt(i));
    delay(50);
  }
  //press a button to continue
  return buttonInput();
}

void printSerial(String str)
{
  int len=str.length();
  for (int i=0; i<len; i++)
  {
    Serial.print(str.charAt(i));
    //Serial.print(str.charAt(i));
    delay(20);
  }
  Serial.println();
}

void serialEvent() {
  while (Serial.available()) {
    // get the new byte:
    char inChar = (char)Serial.read();
    // add it to the inputString:
    //inputString += inChar;


    if (inChar != '\n') {
      inputString += inChar;
    }
    Serial.println(inputString);
    // if the incoming character is a newline, set a flag
    // so the main loop can do something about it:
    if (inChar == '\n') {
      stringComplete = true;
    }
  }
}
