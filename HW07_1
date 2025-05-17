#include <BLEDevice.h>
#include <BLEServer.h>
#include <BLEUtils.h>
#include <BLEAdvertising.h>

#define SERVICE_UUID "f47ac10b-58cc-4372-a567-0e02b2c3d479"

void setup() {
  // 시리얼 초기화 (선택)
  Serial.begin(115200);

  // BLE 초기화
  BLEDevice::init("MyESP32_Server");
  BLEServer* pServer = BLEDevice::createServer();
  BLEService* pService = pServer->createService(SERVICE_UUID);

  // 서비스 시작 및 광고 시작
  pService->start();
  BLEAdvertising* pAdv = BLEDevice::getAdvertising();
  pAdv->addServiceUUID(SERVICE_UUID);
  pAdv->start();

  Serial.println("BLE Server 시작");  
}

void loop() {
  // 서버는 광고만 하므로 빈 루프
}
