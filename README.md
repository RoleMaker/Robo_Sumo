# Robo_Sumo


const int pinoServo = 4; // Mude para o pino do ESP32 que você está usando (Ex: GPIO 18)

// Configurações do PWM para o ESP32
const int canalPWM = 0;
const int frequencia = 50; // Servos operam a 50Hz
const int resolucao = 16;  // Resolução de 16 bits (valores de 0 a 65535)

void setup() {
  Serial.begin(115200); // ESP32 usa preferencialmente 115200 bps
  
  // Configura o canal PWM do ESP32
  ledcAttach(pinoServo, frequencia, resolucao);
  
  Serial.println("--- Teste de Servo 360 no ESP32 (ALKS) ---");
}

// Função para enviar os microssegundos corretos no ESP32
void escreverMicrossegundos(int us) {
  // Converte microssegundos para o ciclo de trabalho (duty cycle) de 16 bits
  // 20000 us representa o período total de 50Hz (1/50 = 20ms)
  uint32_t duty = (us * 65535) / 20000;
  ledcWrite(pinoServo, duty);
}

void loop() {
  // 1. Gira no sentido Horário
  Serial.println("Girando no sentido horário...");
  escreverMicrossegundos(1000); 
  delay(3000);

  // 2. Parada (Ponto Neutro)
  Serial.println("Parando o motor...");
  escreverMicrossegundos(1500); 
  delay(2000);

  // 3. Gira no sentido Anti-horário
  Serial.println("Girando no sentido anti-horário...");
  escreverMicrossegundos(2000); 
  delay(3000);

  // 4. Parada antes de reiniciar
  Serial.println("Parando o motor...");
  escreverMicrossegundos(1500); 
  delay(2000);
}
