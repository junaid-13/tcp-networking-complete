## Lab 3 — Watch the TCP Handshake

**Step 1:** Access both containers
```
# In one terminal:
docker exec -it tcp-server bash

# In another terminal:
docker exec -it tcp-client bash
```

**Step 2:** Ensure tcpdump is installed (should be from previous exercises)
```
# In server terminal:
which tcpdump || (apt update && apt install -y tcpdump)

# In client terminal:
which nc || (apt update && apt install -y netcat-openbsd)
```

**Step 3:** Start watching the TCP handshake on the server
```
# In server terminal:
tcpdump -i eth0 -nn tcp port 8080
```

**Step 4:** Establish a TCP connection from the client
```
# In client terminal:
nc 10.10.0.3 8080
```

**What You'll See:**
In the server terminal running tcpdump, you'll observe output conceptually like:
```
CLIENT                         SERVER

     SYN
 ────────────────────────────>

     SYN, ACK
 <────────────────────────────

     ACK
 ────────────────────────────>
```

**Understanding the Handshake:**
Stop thinking of this as three mysterious packets. Think:
- **SYN**: "Here's my initial sequence number."
- **SYN + ACK**: "I received yours. Here's mine."
- **ACK**: "I received yours."

**Verification:**
- The connection should establish successfully (netcat will connect)
- You should see the three packets in tcpdump representing the SYN, SYN-ACK, ACK exchange
- After the handshake, you can type messages in either terminal and see them appear in the other

**Further Exploration:**
- Try stopping the connection (Ctrl+C in either netcat) and observe what packets appear
- Experiment with different source ports by specifying `-p` in netcat
- Try connecting to a non-listening port to see what happens (should see RST packets)

**Questions to Consider:**
1. What do the flags SYN, ACK, and FIN represent in TCP?
2. Why is the initial sequence number randomized for security?
3. What happens if the SYN-ACK packet is lost? How does TCP handle retransmission?
4. How does this three-way handshake prevent old duplicate connections from causing issues?

**Expected Outcome:**
You should be able to visualize and understand the TCP three-way handshake process through direct observation of network packets, making this fundamental concept second nature.