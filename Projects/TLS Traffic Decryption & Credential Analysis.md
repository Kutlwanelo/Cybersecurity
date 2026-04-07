## TLS Traffic Decryption and Credential Analysis
### Scenario

In this investigation, I analyzed encrypted network traffic captured in a `.pcapng` file. The goal was to decrypt TLS traffic using a provided key log file and identify any sensitive information transmitted over the network.
###  Tools Used
* Wireshark
* TLS Key Log File (`ssl-key.log`)
### 🔍 Investigation Process

1. Opened the packet capture file (`randy-chromium.pcapng`) in Wireshark.

2. Configured TLS decryption:

   * Navigated to **Edit → Preferences → Protocols → TLS**
   * Added the `(Pre)-Master-Secret log filename`
   * Loaded the provided `ssl-key.log` file

3. Reloaded the capture to apply decryption settings.

4. Inspected TLS packets:

   * Identified packets labeled as **“Decrypted TLS”**
   * Observed that not all decrypted traffic was immediately readable

5. Located relevant traffic:

   * Scrolled through packets to find **application data**
   * Identified packets containing structured content

6. Followed the stream:

   * Right-clicked packet → **Follow → HTTP Stream**
   * Reconstructed full communication

---

### 🚨 Findings

* Successfully decrypted TLS traffic using the key log file
* Identified sensitive data transmitted within encrypted traffic
* Located login credentials within the captured session

---

### 🧠 Key Insights

* TLS encryption protects data in transit, but if key material is exposed, traffic can be decrypted
* Not all decrypted traffic is immediately readable—analysis requires filtering and pattern recognition
* Identifying meaningful data requires correlating packet behavior, not just relying on labels

---

### 🎯 Conclusion

This investigation demonstrated how encrypted traffic can be analyzed when key material is available. It highlights the importance of protecting cryptographic keys and reinforces the role of analysts in extracting meaningful insights from network data.

---

### 📎 Skills Demonstrated

* Network traffic analysis
* TLS decryption
* Wireshark usage
* Investigative thinking
* Identifying sensitive data in network streams
