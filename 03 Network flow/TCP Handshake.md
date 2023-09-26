## TCP HANDSHAKE :: DEFINITION
- Transmission Control Protocol
- TCP exists in `Layer 4`, along with UDP
- Highly reliable connection protocol through `Positive Acknowledgement with Retransmission (PAR)`
- Data is re-sent if an `acknowledgement` isn’t received
- The layer 4 data is referred to as `segments`, each segment contains a `checksum` for verification upon receipt
- If verification succeeds, an `acknowledgement` is sent
- If verification `fails`, the receiver discards that segment and waits for retransmission

## TCP HANDSHAKE :: IN ACTION
![image](https://github.com/h0x3ein/network-by-doing/assets/75008854/5680e9e0-dbe1-4b52-a8dd-20662c94789a)


## TCP HANDSHAKE :: IN DETAIL
![image](https://github.com/h0x3ein/network-by-doing/assets/75008854/3e2607a0-346c-4282-b503-784ce26deab0)


