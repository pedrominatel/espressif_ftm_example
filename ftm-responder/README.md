| Supported Targets | ESP32-S2 | ESP32-C3 |
| ----------------- | -------- | -------- |

# FTM Responder Example

## Introduction
One of the ways in which WiFi enabled devices can measure their distance to the Access Point is by measuring Wi-Fi Round Trip Time (Wi-Fi RTT). Wi-Fi RTT is the time a WiFi signal takes to travel from Station to an AP. This time is proportional to the actual distance between them. Given the RTT, the distance can be calculated with below simple formula -

> distance = RTT * c / 2
> (Where c is the speed of light)

Wi-Fi RTT is calculated using a procedure called Fine Timing Measurement(FTM). During FTM procedure, a burst of Action frames is transmitted by one device(FTM Responder) to another(FTM Initiator) and each of them is ACK'ed. Hardware in both the devices mark time-of-arrival (TOA) and time-of-departure (TOD) of both Action frame and its ACK. In the end, the FTM Initiator collects the data for all pairs of Action frame and ACK and calculates RTT for each pair with below formula -

> RTT[i] = (T4[i] - T1[i]) - (T3[i] - T2[i]) Where
> T1[i] : TOD of i'th Action frame from Responder
> T2[i] : TOA of i'th Action frame at Initiator
> T3[i] : TOD of i'th ACK from Initiator
> T4[i] : TOA of i'th ACK at Responder

Average RTT is calculated over all such pairs to get a more accurate result.
Use this example to perform FTM between a Station and a SoftAP or en external AP that supports FTM Responder mode. Both Station and SoftAP need to be run on the supported ESP targets that support FTM and have it enabled.

## How to use example

## Example Output
Example output of an FTM Procedure -

```bash
...
...
```

The final statement gives the average calculated RTT along with an estimated distance between the Station and the AP. This distance is measured by first adjusting the RTT with any physical analog delays and a calibration delta. Distances measured using RTT are not perfectly accurate, and are subjected to various errors like RF interference, multi-path, path loss, orientations etc.
The design requires line-of-sight with straightforward propagation path with no less than -70dBm RSSI for better results.
