
# SMPP v3.4

For customers requiring low-level control of [SMS messaging](https://www.easysendsms.com/bulksms) and the lowest possible latency, we offer our Enhanced SMPP service. 

To use this service, you must contact our [support team](https://www.easysendsms.com/contact-us) to have your SMPP server IP whitelisted.

This document provides a reference for all features available via the SMPP interface for sending SMS. SMPP is the industry standard for sending SMS to network providers and is our native protocol.

The Short Message Peer-to-Peer (SMPP) is a protocol used by the telecommunications industry for exchanging SMS messages between Short Message Service Centers (SMSC) and External Short Messaging Entities (ESME). SMPP is a level-7 TCP/IP protocol that allows for the fast delivery of SMS messages.

## SMPP Versions

The most commonly used versions of SMPP are:
- **v3.3**: The most widely supported standard.
- **v3.4**: Adds transceiver support, allowing single connections to send and receive messages. Data exchange may be synchronous (waiting for a response for each PDU sent) or asynchronous (multiple requests issued in one go, acknowledged in skew order by the other peer).

> **Note:** If your SMPP system supports only passwords up to 8 characters (SMPP v3.4 standard), please contact our [Support team](https://www.easysendsms.com/contact-us) to adjust the password strength settings on your account.

We support throughput up to 500 SMS/sec. For more details, contact our [support](https://www.easysendsms.com/contact-us).

## SMPP Binding

| Description     | Value                                                                                                             |
|-----------------|-------------------------------------------------------------------------------------------------------------------|
| **Host**        | `smpp.easysendsms.com`                                                                                            |
| **Port**        | `2777`                                                                                                            |
| **Secured Port**| `2778`                                                                                                            |
| **Mode**        | TX / RX / TRX                                                                                                     |
| **Connections** | Max 2 connections                                                                                                 |
| **Throughput**  | 30/sec (Support up to 500 SMS/sec, contact [support](https://www.easysendsms.com/contact-us) for further details).|
| **Dest TON**    | Unknown = 0<br />International = 1<br />National = 2<br />Network Specific = 3<br />Subscriber Number = 4<br />Alphanumeric = 5<br />Abbreviated = 6 |
| **Dest NPI**    | Unknown = 0<br />ISDN/telephone numbering plan (E163/E164) = 1<br />Data numbering plan (X.121) = 3<br />Telex numbering plan (F.69) = 4<br />Land Mobile (E.212) = 6<br />National numbering plan = 8<br />Private numbering plan = 9<br />ERMES numbering plan (ETSI DE/PS 3 01-3) = 10<br />Internet (IP) = 13<br />WAP Client Id (to be defined by WAP Forum) = 18<br /><br />If the sender address is alphanumeric or non-numeric, set TON to 5 and NPI to 0.<br />If the sender address is a short code, set TON to 3 and NPI to 0.<br />If the sender starts with a "+", set TON to 1 and NPI to 1.<br />If the recipient starts with a "+", set TON to 1 and NPI to 1.<br />Otherwise, set TON to 0 and NPI to 1. |

## SMPP Status Codes

| Code | Description            |
|------|------------------------|
| 0    | Message sent           |
| 1    | Failed message delivery|
| 2    | Message delivered      |
| 5    | Failed message delivery|

## SMPP Error Codes

| Hex         | Decimal | Description                                | Possible Solution                                                                                                                                                        |
|-------------|---------|--------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000000  | 0       | No Error                                   |                                                                                                                                                                          |
| 0x00000001  | 1       | Message length is invalid                  | Max 140 octets; 160 characters in uncompressed default character encoding.                                                                                               |
| 0x00000002  | 2       | Command length is invalid                  |                                                                                                                                                                          |
| 0x00000003  | 3       | Invalid Command ID                         |                                                                                                                                                                          |
| 0x00000004  | 4       | Incorrect BIND Status for given command    | You must bind first before any other request is handled.                                                                                                                 |
| 0x00000005  | 5       | ESME Already in Bound State                | Do not send bind requests when already bound.                                                                                                                            |
| 0x00000006  | 6       | Invalid Priority Flag                      |                                                                                                                                                                          |
| 0x00000007  | 7       | Invalid Registered Delivery Flag           |                                                                                                                                                                          |
| 0x00000008  | 8       | System Error                               |                                                                                                                                                                          |
| 0x0000000A  | 10      | Invalid Source Address                     |                                                                                                                                                                          |
| 0x0000000B  | 11      | Invalid Dest Addr                          | Invalid length; the length was greater than 3 and less than 17, invalid international format.                                                                            |
| 0x0000000C  | 12      | Message ID is invalid                      |                                                                                                                                                                          |
| 0x0000000D  | 13      | Bind Failed                                |                                                                                                                                                                          |
| 0x0000000E  | 14      | Invalid Password                           |                                                                                                                                                                          |
| 0x0000000F  | 15      | Invalid System ID                          |                                                                                                                                                                          |
| 0x00000015  | 32      | Invalid Service Type                       | Set to NULL                                                                                                                                                              |
| 0x00000033  | 51      | Invalid number of destinations             |                                                                                                                                                                          |
| 0x00000034  | 52      | Invalid Distribution List name             |                                                                                                                                                                          |
| 0x00000040  | 64      | Destination flag is invalid (submit_multi) |                                                                                                                                                                          |
| 0x00000042  | 66      | Invalid submit with replace request        | submit_sm with replace_if_present_flag set                                                                                                                               |
| 0x00000043  | 67      | Invalid esm_class field data               |                                                                                                                                                                          |
| 0x00000044  | 68      | Cannot Submit to Distribution List         |                                                                                                                                                                          |
| 0x00000045  | 69      | submit_sm or submit_multi failed           |                                                                                                                                                                          |
| 0x00000048  | 72      | Invalid Source address TON                 | Accepts International, Network, or Alphanumeric; values of 0x01, 0x03, and 0x05.                                                                                         |
| 0x00000049  | 73      | Invalid Source address NPI                 | Set to null for default value or 0x01 for ISDN numbering plan indicator.                                                                                                 |
| 0x00000050  | 80      | Invalid Destination address TON            | Accepts either Unknown or International; values: 0x00 and 0x01                                                                                                           |
| 0x00000051  | 81      | Invalid Destination address NPI            | Accepts either Unknown or ISDN E163/E164; values: 0x00 and 0x01.                                                                                                         |
| 0x00000058  | 88      | Throttling error                           | ESME has exceeded allowed message limits.                                                                                                                                |
| 0x00000061  | 97      | Invalid Scheduled Delivery Time            |                                                                                                                                                                          |
| 0x00000062  | 98      | Invalid message validity period            | Expiry time.                                                                                                                                                             |
| 0x00000063  | 99      | Predefined Message Invalid or Not Found    | Does not support canned messages; set to NULL.                                                                                                                           |
| 0x00000064  | 100     | ESME Receiver Temporary App Error Code     |                                                                                                                                                                          |
| 0x00000065  | 101     | ESME Receiver Permanent App Error Code     |                                                                                                                                                                          |
| 0x00000066  | 102     | ESME Receiver Reject Message Error Code    |                                                                                                                                                                          |
| 0x00000067  | 103     | query_sm request failed                    |                                                                                                                                                                          |
| 0x000000C0  | 192     | Error in the optional part of the PDU Body |                                                                                                                                                                          |
| 0x000000C1  | 193     | Optional Parameter not allowed             |                                                                                                                                                                          |
| 0x000000C2  | 194     | Invalid Parameter Length                   |                                                                                                                                                                          |
| 0x000000C3  | 195     | Expected Optional Parameter missing        |                                                                                                                                                                          |
| 0x000000C4  | 196     | Invalid Optional Parameter Value           | This error occurs when an optional value parameter retrieve fails; this is not normal behavior.                                                                          |
| 0x000000FE  | 245     | Delivery Failure                           | Used for data_sm_resp.                                                                                                                                                   |
| 0x000000FF  | 255     | Unknown Error                              |                                                                                                                                                                          |
| 0x0000012F  | 303     | Country/Network not available              |                                                                                                                                                                          |

