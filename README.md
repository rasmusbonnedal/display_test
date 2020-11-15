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
10. Tryck på pilknappen på menyraden (Upload). ~När det står "Connecting..." håll inne BOOT-knappen tills texten börjar rulla. När den är klar (Hard resetting via RTS pin..." tryck på EN för att resetta modulen.~ Nu ska det stå "Hej från Arduino!" i serial monitorn.
11. Grattis, nu är allting klart för att köra.

## Displayen
Displayen är monokrom (svart-vit) och har 128x64 punkter. För att använda den gör man följande:
1. Gå till Tools > Library Manager, sök efter "ESP32 OLED Driver".
2. Installera "ESP8266 and ESP32 OLED driver for SSD1306 displays" från ThingPulse.
```
#include "SSD1306Wire.h"

SSD1306Wire display(0x3c, 5, 4);

void setup() {
  Serial.begin(115200);
  display.init();
  Serial.println("Hej från Display!");
}

void loop() {
  display.clear();
  display.drawString(0, 0, "Hallå display!");
  display.drawString(0, 10, "Här är jag!");
  display.display();
  delay(100);
}
```
3. Tryck på pilknappen på menyraden (Upload). ~När det står "Connecting..." håll inne BOOT-knappen tills den röda texten börjar rulla.~
4. Nu ska text komma upp på displayen!

## Kopplingsbord
Kallas också för breadboard. På breadborden kan man koppla ihop komponenter med varandra och till modulen med hjälp av sladdar. För att underlätta är breadboarden ihopkopplad inuti också.

| ![Breadbord](Breadboard-Pic.jpg) |
| :--: |
| *Breadboard* |

På breadboardens ovansida och undersida finns en röd (+) och en blå (-) linje som visar hur de sitter ihop. Sedan är för varje siffra i en kolumn alla fem punkter A-E och F-J ihopkopplade var för sig.

| ![Koppling inuti](breadboard.png) |
| :--: |
| *Kopplingar inuti* |

Det är på breadboardet vi kopplar ihop våra experiment.

## 1. Lysdioder
En lysdiod är en komponent som släpper igenom ström åt ett håll och då lyser den. Det längre av de två benen är positiv (+) och det korta är negativ (-). I det här experimentet ska vi koppla in en lysdiod till en av modulens datapinnar och blinka med den. För att det inte ska komma för mycket ström genom dioden och riskera att skada modulen eller lysdioden ska vi också ha ett motstånd.

### Datapinnar
Modulen har en massa datapinnar som är numrerade. De kan ställas in från programmet att antingen vara digitala (av eller på) eller analoga (de kan ge ifrån sig eller läsa av olika spänningsnivåer). De kan också ställas in att vara i ut-läge (de ger ifrån sig spänning) eller in-läge (de detekterar spänning som kommer in). I det här läget ska vi göra en pinne digital och i ut-läge för att styra lysdioden.

1. Koppla en svart sladd från GND på modulen (GND är förkortning för ground vilket betyder jord. Det är vad man kallar den negativa (-) polen.) till den ett hål på den blåa linjen på breadboarden.
2. Koppla en annan sladd (i exemplet gul) från pin 16 på modulen (Det är den pinne vi ska använda som utpinne) till en plats i kolumn 0 på breadboarden.
3. Sätt i en lysdiod med det långa benet i kolumn 0 och det korta i kolumn 1. Nu är lysdiodens pluspol ihopkopplad med pin 16 på modulen med hjälp av breadboarden och den gula sladden.
4. Sätt ett motstånd på 1000 ohm mellan kolum 1 (samma som lysdiodens minuspol) och kolumn 6.
5. Koppla en svart sladd från kolumn 6 (motståndets andra ben) och den blåa linjen där uppe. Nu är kretsen kopplad och när modulen lägger spänning på pinne 16 kommer ström flyta genom den gula sladden, genom lysdioden, genom motståndet och till slut genom de två svarta sladdarna till modulens minuspol.
