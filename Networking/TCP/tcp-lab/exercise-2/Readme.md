## Lab 2 — Explore TCP Communication

**Step 1:** Access both containers
```
# In one terminal:
docker exec -it tcp-server bash

# In another terminal:
docker exec -it tcp-client bash
```

**Step 2:** Install TCP analysis tools on both containers
```
# In server terminal:
apt update
apt install -y net-tools tcpdump netcat-openbsd

# In client terminal:
apt update
apt install -y net-tools tcpdump netcat-openbsd
```

**Step 3:** Test TCP communication
```
# In server terminal (start listener):
nc -l -p 8080

# In client terminal (connect to server):
nc 10.10.0.3 8080
```

**Verification:**
- Type a message in the client terminal and press Enter
- You should see it appear in the server terminal
- Type a message in the server terminal and press Enter
- You should see it appear in the client terminal

**Further Exploration:**
- Use `netstat -tanp | grep :8080` in either container to view TCP connection states
- Use `tcpdump -i any port 8080 -vv` to capture and analyze TCP packets
- Observe the TCP three-way handshake (SYN, SYN-ACK, ACK) in the packet capture
- Notice what happens when you terminate the connection (Ctrl+C in either netcat)