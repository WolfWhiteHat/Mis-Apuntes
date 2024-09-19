tshark -r Wifi_traffic.pcap -Y "wlan"
![[Pasted image 20240315122556.png]]
![[Pasted image 20240315122537.png]]


tshark -r WiFi_traffic.pcap -Y "wlan.fc.type_subtype==0x000c"
![[Pasted image 20240315122650.png]]

tshark -r WiFi_traffic.pcap -Y "eapol"
![[Pasted image 20240315122817.png]]


tshark -r WiFi_traffic.pcap -Y "wlan.fc.type_subtype==8" -Tfields -e wlan.ssid -e wlan.bssid
![[Pasted image 20240315122941.png]]
![[Pasted image 20240315123000.png]]


tshark -r WiFi_traffic.pcap -Y "wlan.ssid==LazyArtists" -Tfields -e wlan.bssid
![[Pasted image 20240315123102.png]]


tshark -r WiFi_traffic.pcap -Y "wlan.ssid==Home_Network" -Tfields -e wlan_radio.channel
![[Pasted image 20240315123302.png]]
![[Pasted image 20240315123327.png]]


tshark -r WiFi_traffic.pcap -Y "wlan.fc.type_subtype==0x000c" -Tfields -e wlan.ra
![[Pasted image 20240315123425.png]]


tshark -r WiFi_traffic.pcap -Y "wlan.ta== 5c:51:88:31:a0:3b && http" -Tfields -e http.user_agent
![[Pasted image 20240315124130.png]]

