# Check-Point-1---Edge-Computing
int ledVerde = 13;                      - aqui estou falando que o led verde esta no pin 13 
int ledAmarelo = 12;                    - aqui estou falando que o amarelo esta no pin 12
int ledVermelho = 11;                   - aqui estou falando que o vermelho esta no pin 11
int ldrPIN = A0;                        - aqui estou falando que o ldr esta no pin A0
int buzzer = 8;                         - aqui estou falando que o BUZZER esta no pin 8 

void setup() {
  pinMode(ledVerde, OUTPUT);            - aqui estou configurando o led verde como saída
  pinMode(ledAmarelo, OUTPUT);          - aqui estou configurando o led amarelo como saída
  pinMode(ledVermelho, OUTPUT);         - aqui estou configurando o led vermelho como saída
  pinMode(buzzer, OUTPUT);              - aqui estou configurando o buzzer como saída
  Serial.begin(9600);                   - aqui estou iniciando a comunicação serial com a velocidade 9600
}

void loop() {
  int valorLuz = analogRead(ldrPIN);    - aqui estou lendo o valor analógico do LDR
  valorLuz = map(valorLuz, 0, 1023, 0, 100);        - aqui estou convertendo o valor do LDR para uma escala de 0 a 100%
  Serial.println(valorLuz);             - aqui estou imprimindo o valor da luz no monitor serial

  if (valorLuz > 66) {                  - se a intensidade da luz for maior que 66% ele vai ligar o led vermelho e o buzzer
    digitalWrite(ledVerde, LOW);
    digitalWrite(ledAmarelo, LOW);
    digitalWrite(ledVermelho, HIGH);
    digitalWrite(buzzer, HIGH);
    digitalWrite(buzzer, LOW);          - aqui ele vai desligar 
  }

  else if (valorLuz > 33) {             -  se a intensidade da luz for maior que 33% ele vai ligar apenas o led amarelo 
    digitalWrite(ledVerde, LOW);
    digitalWrite(ledAmarelo, HIGH);
    digitalWrite(ledVermelho, LOW);
    digitalWrite(buzzer, LOW);          - e desligar o buzzer 
  }

  
  else {
    digitalWrite(ledVerde, HIGH);      - caso ele esteja menor que 33% ele paenas vai ligar o led verde e desligar o buzzer
    digitalWrite(ledAmarelo, LOW);
    digitalWrite(ledVermelho, LOW);
    digitalWrite(buzzer, LOW);
  }

  delay(500);                          - aqui estou colocando um atraso de 0,5 segundos antes de repetir o loop
}

