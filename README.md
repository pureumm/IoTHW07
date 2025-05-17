# IoT-HW07
Assignment of IoT HW

BLE-Based Distance Estimation

Environment: Indoor corridor (minimal obstacles), temperature ≈ 22 °C

Hardware:

ESP32 BLE Server broadcasting at txPower = –59 dBm (measured at 1 m)

ESP32 BLE Client scanning and recording RSSI

Path-loss model:![Image](https://github.com/user-attachments/assets/221ae262-4d9d-4043-884d-8e35b456cbe8)Procedure:

Place Server and Client at a fixed separation (0.5 m, 1 m, 2 m, 3 m, 4 m).

At each distance, record 10 RSSI samples on the Client.

Compute estimated distance for each sample via estimateDistance(rssi).

Calculate the mean estimated distance at each true distance.

Summary Table
True Distance (m)	Mean Estimated (m)	Error (m)	Error Rate (%)
0.5	                0.47	            0.03        	6.0
1.0  	              1.12	            0.12        	12.0
2.0  	              2.05	            0.05	        2.5
3.0  	              3.30	            0.30	        10.0
4.0                	3.90	            0.10	        2.5

bar chart
![0](https://github.com/user-attachments/assets/d86e5f3e-377e-4427-b30d-cfb37d96aa1b)
At distances of 2 m and 4 m, the BLE-based estimator achieved its best accuracy, with error rates as low as 2.5 %, whereas at 1 m and 3 m the deviations were larger—up to 10–12 %. Such variations are largely attributable to environmental factors: in our indoor corridor setting, multipath reflections cause the RSSI to fluctuate, and occasional human movement or slight changes in device orientation introduce additional noise. To improve overall performance, we recommend applying a moving-average filter to smooth out rapid RSSI spikes and, for even greater stability, incorporating a Kalman filter to dynamically correct measurement noise. Finally, gathering extra calibration data at intermediate points (for example at 1.5 m and 2.5 m) will allow you to refine both the txPower reference and the path-loss exponent n, further reducing systematic bias.


## HW07_1 : Server Code
![07_1](https://github.com/user-attachments/assets/6b521948-6d93-4c33-b4f9-e96b3749392a)
## HW07_2 : Client Code
![07_2](https://github.com/user-attachments/assets/55c21dd9-eede-41f8-9ce9-1c11f5552009)
## HW07_2_1 : Bouns 1 add
![07_2_1](https://github.com/user-attachments/assets/cb7b8a1b-cbb0-4ed4-8ba3-3e529369522e)
![07_2_1](https://github.com/user-attachments/assets/87a5b1ff-469b-4c2a-8f4b-9db038b5d8be)
## HW07_2_2 : Bonus 2 add
![07_2_2](https://github.com/user-attachments/assets/154f54d6-656c-4a84-bc2b-81da09f79994)


