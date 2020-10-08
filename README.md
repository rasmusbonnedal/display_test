# Elektronikpyssel med Arduino
## Innehåll
* Arduinomodul ESP32 Wroom med SSD1306 OLED 128x64 på i2c

## Förberedelser
1. Ladda ner och installera Arduino Software från https://www.arduino.cc/en/Main/Software “Windows Installer”.
2. Starta Arduino IDE och gå in i File > Preferences. Skriv in https://dl.espressif.com/dl/package_esp32_index.json i “Additional Board Manager URLs”.
3. Gå till Tools > Board > Boards Manager… Sök på esp32 och installera esp32 by Espressif Systems.
4. Välj Tools > Board > ESP32 Arduino > ESP32 Dev Module.
5. Koppla in modulen till datorn med USB och slå switchen till "ON".
6. Välj Tools > Board > Port och välj den COM-porten som finns. Modulen har en USB-serial interface vars driver installeras med Arduino SDK.
7. Öppna Serial Monitor (Tools > Serial Monitor) och ställ in den på 115200 baud.
8. Tryck på EN på modulen, nu ska text från modulen visas i monitorn.
9. Skriv in följande i sketchen och spara:
```
void setup() {
  Serial.begin(115200);
  Serial.println("Hej från Arduino!");
}

void loop() {
}
```
10. Tryck på pilknappen på menyraden (Upload). När det står "Connecting..." håll inne BOOT-knappen tills texten börjar rulla. När den är klar (Hard resetting via RTS pin..." tryck på EN för att resetta modulen. Nu ska det stå "Hej från Arduino!" i serial monitorn.
11. Grattis, nu är allting klart för att köra.
