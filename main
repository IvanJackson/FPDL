#include <LiquidCrystal.h>

#define LED0 8
#define LED1 9
#define LED2 10
#define LED3 11
#define LED4 12
#define LED5 13
#define NUMLED 6

#define ANALOGPIN A0

int LED[] = {LED0,LED1,LED2,LED3,LED4,LED5};

void displayLED(){
  
  //Turn all LEDs off
  for(int i = 0; i < NUMLED; i++){
  	digitalWrite(LED[i], HIGH);
  }
  
  //Calculate which LEDs will turn on based on signal amplitude
  double percentageOn = (double)((double)(analogRead(ANALOGPIN))/1023);
  int NUMON = (int)((NUMLED+1)*percentageOn);
  if(NUMON > NUMLED) NUMON = NUMLED;
  
  //Turn on LEDs depending on volume
  for(int i = 0; i < NUMON; i++){
  	digitalWrite(LED[i], LOW);
  }
  
}

LiquidCrystal lcd(1, 2, 4, 5, 6, 7);

byte smiley[8] = {
  B00000,
  B10001,
  B00000,
  B00000,
  B10001,
  B01110,
  B00000,
};

byte frownie[8]={
  B00000,
  B10001,
  B00000,
  B00000,
  B01110,
  B10001,
  B00000,
};

byte surprised[8]={
  B10001,
  B00000,
  B00100,
  B01010,
  B10001,
  B01010,
  B00100,
};

byte wave[8] = {
  B10000,
  B11000,
  B10000,
  B10000,
  B11000,
  B11000,
  B10000,
};

byte wave1[8] = {
  B11000,
  B11100,
  B11100,
  B11000,
  B11100,
  B11000,
  B111000,
};

byte wave2[8] = {
  B11100,
  B11110,
  B11110,
  B11100,
  B11110,
  B11100,
  B11110,
};

byte wave3[8] = {
  B11111,
  B11111,
  B11111,
  B11110,
  B11111,
  B11110,
  B11111,
};


byte wave4[8] = {
  B11111,
  B11111,
  B11111,
  B11111,
  B11111,
  B11111,
  B11111,
};

byte sq[8] = {
  B00000,
  B00000,
  B01110,
  B01110,
  B01110,
  B01110,
  B00000,
};
  
int pastWaves =0;

void setup() {
  
  //Setup LED pins
  for(int i = 0; i < NUMLED; i++){
  	pinMode(LED[i], OUTPUT);
  }

  lcd.createChar(0, wave);
  lcd.createChar(1,wave1);
  lcd.createChar(2,wave2);
  lcd.createChar(3,wave3);
  lcd.createChar(4,wave4);
  lcd.createChar(5,sq);
  lcd.createChar(6,smiley);
  lcd.createChar(7,frownie);
  lcd.createChar(8,surprised);
  
  lcd.begin(16, 2);
}

void waves() {
  for(int i=0;i<16;i++){
  //loop to repeat on every column
  	int speed = powerCalculator();
    
    if(pastWaves!=0){
      for(int count=0;count<pastWaves;count++){
      	   lcd.setCursor(count,0);
           lcd.write(byte(4));
           lcd.setCursor(count,1);
           lcd.write(byte(4));
      }
    }
      
    //keeping on the waves before us and keep it moving forward
    for(int waveNumber =0;waveNumber<5;waveNumber++){
      //to paint each different wave state
      if(pastWaves!=0){
        for(int count=0;count<pastWaves;count++){
          lcd.setCursor(count,0);
          lcd.write(byte(4));
          lcd.setCursor(count,1);
          lcd.write(byte(4));
        }
      }
      lcd.setCursor(i,0);
      lcd.write(byte(waveNumber));
      lcd.setCursor(i,i+1);
      lcd.write(byte(waveNumber));
      

      busyWait(speed);
      //delay((1000*speed)+175);
      
      lcd.clear();

      int speed = powerCalculator();

      busyWait(speed);
      //delay((1000*speed)+175);
    }
    pastWaves++;
  }
  lcd.clear();
  pastWaves=0;
}

void squares(){
  int squares=0;
  for(int i=0;i<100;i++){
    int column = random(16);
    int row = random(2);
    
    lcd.setCursor(column,row);
    lcd.write(byte(5));


    int speed = powerCalculator();

    busyWait(speed);
    //delay((1000*speed)+175);
    squares++;
    
    if(squares==10){
      lcd.clear();
      squares=0;
  	}
  }
}

void faces(){
  int rand = random(2);
  //going left to right
  if(rand==0){
    for(int row=0;row<2;row++){
      for(int column=0;column<16;column++){
        
		lcd.setCursor(column,row);
        
        int face = random(3);
        
        if(face==0)  //smile
          lcd.write(byte(6));
        
        if(face==1)  //frown
          lcd.write(byte(7));
        
        else   //surprised
          lcd.write(byte(8));
        
        int speed = powerCalculator();

        busyWait(speed);
        //delay((1000*speed)+175);
      }
    }
  }
  else {
    for(int row=1;row>=0;row--){
      for(int column=15;column>=0;column--){
        
		lcd.setCursor(column,row);
        
        int face = random(3);
        
        if(face==0)  //smile
          lcd.write(byte(6));
        
        if(face==1)  //frown
          lcd.write(byte(7));
        
        else //surprised
          lcd.write(byte(8));
        
        int speed = powerCalculator();

        busyWait(speed);
        //delay((1000*speed)+175);
          
      }
    }
  }
}

//to change the speed of the desings, using the potentiometers
int powerCalculator(){
  int power = analogRead(A0);
  return ((double)power / 1023);
}

void busyWait(int gspeed){
  unsigned long start = millis();
  while (millis()-start < (1000*gspeed)){
          displayLED();
  }
}

void loop() {
  //Display amplitude on LED
  displayLED();
  
  //Determine the LCD algorithm
  int rand = random(3);
  if(rand==0)
    waves();
  if(rand==1)
  	squares();
  else
  	faces();
 }
