#include <BLEDevice.h>
#include <BLEScan.h>

#define SERVICE_UUID   "f47ac10b-58cc-4372-a567-0e02b2c3d479"
const int LED_PIN      = 2;
const double THRESHOLD = 0.5;    // 0.5 m 이내일 때

BLEScan* pBLEScan;

double estimateDistance(int rssi) {
  const int txPower = -59;
  const double n    = 2.0;
  return pow(10.0, (txPower - rssi) / (10.0 * n));
}

void setup() {
  Serial.begin(115200);
  pinMode(LED_PIN, OUTPUT);

  BLEDevice::init("");
  pBLEScan = BLEDevice::getScan();
  pBLEScan->setActiveScan(true);
}

void loop() {
  // 1) BLE 스캔
  BLEScanResults* res = pBLEScan->start(3, false);
  bool near = false;

  // 2) 결과 처리
  for (int i = 0, cnt = res->getCount(); i < cnt; i++) {
    auto dev = res->getDevice(i);
    if (dev.haveServiceUUID() && dev.isAdvertisingService(BLEUUID(SERVICE_UUID))) {
      double d = estimateDistance(dev.getRSSI());
      near = (d <= THRESHOLD);
      Serial.print("dis: ");
      Serial.print(d, 2);
      Serial.println(" m");
      break;
    }
  }

  // 3) 메모리 해제
  pBLEScan->clearResults();

  // 4) LED 빠른 블링크 (100 ms 주기, 50 ms on/off)
  if (near) {
    digitalWrite(LED_PIN, (millis() % 100) < 50 ? HIGH : LOW);
  } else {
    digitalWrite(LED_PIN, LOW);
  }

  delay(20);
}
