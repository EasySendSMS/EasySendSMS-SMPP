# SMPP v3.4

For our customers that require low level control of [SMS messaging](https://www.easysendsms.com/bulksms) and lowest possible latency we offer our Enhanced SMPP service

You need to reach out to our support team to get your SMPP server ip white listed to use this service.

This document provides a reference for all features available to you via the SMPP interface for sending SMS. SMPP is considered the industry standard for sending SMS to Network providers and is our native protocol.

The Short Message Peer-to-Peer (SMPP) is a protocol used by the telecommunications industry for exchanging SMS messages between Short Message Service Centers (SMSC) and/or External Short Messaging Entities (ESME).

The protocol is a level-7 TCP/IP protocol, which allows fast delivery of SMS messages. The most commonly used versions of SMPP are v3.3, the most widely supported standard, and v3.4, which adds transceiver support (single connections that can send and receive messages). Data exchange may be synchronous, where each peer must wait for a response for each PDU being sent, and asynchronous, where multiple requests can be issued in one go and acknowledged in a skew order by the other peer.

## NOTE: If your SMPP system supports only passwords up to 8 characters (SMPP v3.4 standard), contact our Support team to adjust the password strength settings on your account.

## We support throughput up to 500 SMS/Sec, for that you can contact our [support](https://www.easysendsms.com/contact-us) for further details.


### SMPP Binding:

| Description | Value |
| ----------- | ----- |
| Host | smpp.easysendsms.com |
| Port | 2777 |
| Secured Port | 2778 |
| Mode | TX / RX / TRX |
| Connections | max 2 connections |
| Throughput | 30/Sec. ( We support up to 500 SMS/Sec, contact our [support](https://www.easysendsms.com/contact-us) for further details). |
| Dest TON | Unknown = 0<br />International = 1<br />National = 2<br />Network Specific = 3<br />Subscriber Number = 4<br />Alphanumeric = 5<br />Abbreviated = 6 |
| DEST NPI | Unknown = 0<br />ISDN/telephone numbering plan (E163/E164) = 1<br />Data numbering plan (X.121) = 3<br />Telex numbering plan (F.69) = 4<br />Land Mobile (E.212) =6<br />National numbering plan = 8<br />Private numbering plan = 9<br />ERMES numbering plan (ETSI DE/PS 3 01-3) = 10<br />Internet (IP) = 13<br />WAP Client Id (to be defined by WAP Forum) = 18<br /><br />If the sender address is alphanumeric (contains both letters and numbers) or non-numeric, TON is set to 5 and NPI to 0.<br />If the sender address is a short code, TON is set to 3, and NPI is set to 0.<br />If the sender starts with a â€œ+â€, TON is set to 1, and NPI is set to 1.<br />If the recipient starts with a â€œ+â€, TON is set to 1, and NPI is set to 1.<br />Otherwise, TON is set to 0 and NPI is set to 1. |


### SMPP Binding:

| Code | Description |
| ---- | ----------- |
| 0 | Message sent |
| 1 | Failed message delivery |
| 2 | Message delivered |
| 5 | Failed message delivery |


### SMPP Error Codes:

| Hex | Decimal | Description | Possible Solution |
| --- | ------- | ----------- | ----------------- |
|  |  | 0x000000C5-0x000000FD |  |
| 0x00000000 | 0 | No Error |  |
| 0x00000001 | 1 | Message length is invalid | Max 140 octets; 160 chars in uncompressed default character encoding. |
| 0x00000002 | 2 | Command length is invalid |  |
| 0x00000003 | 3 | Invalid Command ID |  |
| 0x00000004 | 4 | Incorrect BIND Status for given command | You must bind first before any other request is handled. |
| 0x00000005 | 5 | ESME Already in Bound State | Do not send bind requests when already bound. |
| 0x00000006 | 6 | Invalid Priority Flag |  |
| 0x00000007 | 7 | Invalid Registered Delivery Flag |  |
| 0x00000008 | 8 | System Error |  |
| 0x00000009 |  | Reserved |  |
| 0x0000000A | 10 | Invalid Source Address |  |
| 0x0000000B | 11 | Invalid Dest Addr | Invalid length; the length was greater than 3 && less than 17, invalid international format. |
| 0x0000000C | 12 | Message ID is invalid |  |
| 0x0000000D | 13 | Bind Failed |  |
| 0x0000000E | 14 | Invalid Password |  |
| 0x0000000F | 15 | Invalid System ID |  |
| 0x00000010 | 16 | Reserved |  |
| 0x00000011 | 17 | Cancel SM Failed |  |
| 0x00000012 |  | Reserved |  |
| 0x00000013 | 19 | Replace SM Failed |  |
| 0x00000014 | 20 | Message Queue Full |  |
| 0x00000015 | 32 | Invalid Service Type | Set to NULL |
| 0x00000016 |  | Reserved thru -0x00000032 |  |
| 0x00000033 | 51 | Invalid number of destinations |  |
| 0x00000034 | 52 | Invalid Distribution List name |  |
| 0x00000035 | 53 | Reserved thru -0x0000003F |  |
| 0x00000040 | 64 | Destination flag is invalid (submit_multi) |  |
| 0x00000041 |  | Reserved |  |
| 0x00000042 | 66 | Invalid submit with replace request; submit_sm with replace_if_present_flag set |  |
| 0x00000043 | 67 | Invalid esm_class field data |  |
| 0x00000044 | 68 | Cannot Submit to Distribution List |  |
| 0x00000045 | 69 | submit_sm or submit_multi failed |  |
| 0x00000046 |  | Reserved thru -0x00000047 |  |
| 0x00000048 | 72 | Invalid Source address TON | Accepts International, Network, or Alphanumeric; values of 0x01, 0x03, and 0x05. |
| 0x00000049 | 73 | Invalid Source address NPI | Set to null for default value or 0x01 for ISDN numbering plan indicator. |
| 0x00000050 | 80 | Invalid Destination address TON | Accepts either Unknown Or International; values: 0x00 and 0x01 |
| 0x00000051 | 81 | Invalid Destination address NPI | Accepts either Unknown Or ISDN E163/E164: values: 0x00 and 0x01. |
| 0x00000052 |  | Reserved |  |
| 0x00000053 | 83 | Invalid system_type field |  |
| 0x00000054 | 84 | Invalid replace_if_present flag. |  |
| 0x00000055 | 85 | Invalid number of messages |  |
| 0x00000056 |  | Reserved thru -0x00000057 |  |
| 0x00000058 | 88 | Throttling error; ESME has exceeded allowed message limits. |  |
| 0x00000059 | 89 | Reserved thru -0x00000060 |  |
| 0x00000061 | 97 | Invalid Scheduled Delivery Time |  |
| 0x00000062 | 98 | Invalid message validity period (Expiry time). |  |
| 0x00000063 | 99 | Predefined Message Invalid or Not Found | Does not support canned messages; set to NULL. |
| 0x00000064 | 100 | ESME Receiver Temporary App Error Code |  |
| 0x00000065 | 101 | ESME Receiver Permanent App Error Code |  |
| 0x00000066 | 102 | ESME Receiver Reject Message Error Code |  |
| 0x00000067 | 103 | query_sm request failed |  |
| 0x00000068 | 104 | Reserved thru -0x000000BF |  |
| 0x000000C0 | 192 | Error in the optional part of the PDU Body |  |
| 0x000000C1 | 193 | Optional Parameter not allowed |  |
| 0x000000C2 | 194 | Invalid Parameter Length |  |
| 0x000000C3 | 195 | Expected Optional Parameter missing. |  |
| 0x000000C4 | 196 | Invalid Optional Parameter Value | This error occurs when an optional value parameter retrieve fails; this not normal behavior. |
| 0x000000FE | 245 | Delivery Failure, used for data_sm_resp |  |
| 0x000000FF | 255 | Unknown Error |  |
| 0x00000100 |  | Reserved for SMPP extension thru -0x000003FF |  |
| 0x0000012F | 303 | Country/Network not available |  |
