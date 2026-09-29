// C++ code
// Três variavel do tipo inteira 

int nivelAgua=0;
int interruptor= 0;
int bomba=0;


void setup()
{
  
  
Serial.begin(9600);
pinMode(7,INPUT);// INTERRUPTOR
pinMode(6,OUTPUT);// LED VERMELHO E RESISTOR
pinMode(5,OUTPUT);// LED VERDE E RESISTOR
pinMode(4,OUTPUT);// LED AZUL E RESISTOR
pinMode(3,OUTPUT);// PIEZO 
  
  
}

void loop()
{
  
  //Bloco de agua 
  
  if (nivelAgua!=0)
    
    nivelAgua-=1;
  
  
  //Bloco do Interrupator
    
    interruptor = digitalRead(7); 
   
  if ( interruptor==HIGH){
    
    
    digitalWrite(6,LOW); // LED VERMELHO DELISGADO
    digitalWrite(5,HIGH);//LED VERDE LIGADO 
    
    //BLOCO DO BOBEAMENTO
    //
  }
    if (nivelAgua>=30){
    bomba=0;
    digitalWrite(3,LOW);// DESLIGO PIEZO
    digitalWrite(4,LOW);// DESLIGO AZUL
    Serial.print("Bomba Desligada");
      //BOIA 1
      Serial.println("NIVEL DE AGUA DIMINUINDO");
    
    }
     
    if (nivelAgua<=15){
    
    bomba=1; 

     Serial.print("Bomba Ligada ");
      //BOIA 2
    
    
    
    }
    
    //Bloco de bomba 
    if (bomba==1){
     nivelAgua+=2;
    digitalWrite(3, HIGH); // LIGADO PIEZO 
    digitalWrite(4,HIGH); // LIGA LED VERMELHO
    digitalWrite(5,HIGH);
    tone(3,250,200); // PORTA 3, TOM , DURAÇÃO DO BARULO
       
    Serial.println("Bombeando a Agua: ");
    
    
    
}
  
  else {
   bomba=0; 
    digitalWrite(6,HIGH); // LED VERMELHO LIGA 
    digitalWrite(5,LOW);// LED VERDE DESLIGA 
     digitalWrite(4,LOW); // LED VERMELHO DESLIGA
    digitalWrite(3,LOW); // PIEZO DESLIGA 
   
  
  }
   
  Serial.print("***NIVEL DE AGUA***: ");
  Serial.println(nivelAgua);
  
  
  delay(400);
   
}
