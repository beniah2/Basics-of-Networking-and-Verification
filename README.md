**Story:**  
You just joined the cybersecurity operations team at a digital forensics lab. Your task for the day is to verify that your Kali workstation can communicate with the internal gateway before starting packet capture exercises. The network admin has given you a test IP to assign to your interface for lab verification. You will confirm the interface setup, assign the IP, view the routing table, and test connectivity using ping.

---

**Action Steps:**

1. **Show all network interfaces**  
 You begin by listing all interfaces to identify your primary adapter (`eth0` in this case).

**Command:** ip addr show

![[Pasted image 20251006153532.png]]

---

2.  **Activate the interface (if down)**  
If your interface shows `state DOWN`, activate it. But, as shown above,the  state UP shows the interface is up and running.

**Command**: sudo ip link set dev lo up

<img width="951" height="153" alt="image" src="https://github.com/user-attachments/assets/0321cbf0-e13f-43f8-91e5-dac2af7b7a27" />


---

3. **Assign a test IP address**  
You add a temporary test IP to the interface.

**Command**: sudo ip addr add 10.0.0.100/24 dev lo

<img width="1098" height="208" alt="image" src="https://github.com/user-attachments/assets/eff2e966-1206-4619-b1ca-a1e41fe9ec8a" />


This assigns IP `10.0.0.100` with a subnet mask of `/24` to the loopback interface displayed as "lo".

---

4. **Verify the IP address assignment**  
You confirm that the new IP is now active on the interface.

**Command**: ip addr show dev lo

<img width="1350" height="370" alt="image" src="https://github.com/user-attachments/assets/1e2e6a72-da2d-4d10-bb1f-fbceac406bde" />


---

5. **View routing table**  
You check the network routes to verify the gateway and reachable networks.

**Command**: ip route show

<img width="1343" height="177" alt="image" src="https://github.com/user-attachments/assets/fb6afbe8-c997-47f2-8eb1-03ded5811a10" />


---

6. **Ping the gateway to confirm connectivity**  
You test if your interface can reach the gateway.

**Command**: ping -c 3 10.0.0.1

<img width="1177" height="405" alt="image" src="https://github.com/user-attachments/assets/2a98b41a-3c29-46a3-8642-c1b426411c34" />


---

7. **List active listening ports and services**  
 You quickly review which services are listening on your Kali system.

**Command**: ss -tuln | head -n 20

<img width="1332" height="145" alt="image" src="https://github.com/user-attachments/assets/518725dc-5f24-4b73-8738-d366fd587bde" />


---

8. **Cleanup**  
After the test, you remove the test IP.

**Command**:  sudo ip addr del 10.0.0.100/24 dev  lo

<img width="1353" height="448" alt="image" src="https://github.com/user-attachments/assets/6c3f028e-4499-4aac-927b-a500d26c54db" />



**Expected Notes:**

- The new IP `10.0.0.100` appears on `eth0`.
    
- The routing table displays a valid default route through `10.0.0.1`.
    
- Ping replies confirm gateway communication.
    
- `ss -tuln` shows open TCP/UDP ports, verifying active network services.
