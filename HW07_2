#include <BLEDevice.h>
#include <BLEScan.h>

#define SERVICE_UUID      "f47ac10b-58cc-4372-a567-0e02b2c3d479"
const int scanTime = 3;       // 스캔 시간 (초)
const int txPower  = -59;     // 서버에서 사용한 txPower 값
const double n     = 3.0;     // 경로손실 지수 (환경에 따라 조정)

BLEScan* pBLEScan;

double estimateDistance(int rssi) {
  return pow(10.0, (txPower - rssi) / (10.0 * n));
}

void setup() {
  Serial.begin(115200);
  BLEDevice::init("");
  pBLEScan = BLEDevice::getScan();
  pBLEScan->setActiveScan(false);
  Serial.println("BLE Client 시작");
}

void loop() {
  // start() 가 포인터를 반환하므로, 포인터로 받습니다.
  BLEScanResults* results = pBLEScan->start(scanTime, false);
  int count = results->getCount();
  for (int i = 0; i < count; i++) {
    BLEAdvertisedDevice dev = results->getDevice(i);
    if (dev.haveServiceUUID() && dev.isAdvertisingService(BLEUUID(SERVICE_UUID))) {
      int rssi = dev.getRSSI();
      double dist = estimateDistance(rssi);
      Serial.print("RSSI: "); Serial.print(rssi);
      Serial.print(" dBm, 거리: "); Serial.print(dist, 2); Serial.println(" m");
    }
  }
  // 스캔 결과 삭제
  pBLEScan->clearResults(); 
  delay(1000);
}
