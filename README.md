# SMPP v3.4

For our customers that require low-level control of [SMS messaging](https://www.easysendsms.com/bulksms) and the lowest possible latency, we offer our Enhanced SMPP service.

EasySendSMS utilizes TLS encryption to guarantee secure communication with our SMPP servers. Since many SMPP client SDKs lack built-in TLS support, you may need to employ a tunneling solution to establish a secure connection between your client and our server.

## SMPP Account Information

An SMPP account includes a regional host connected via secure port `2778`, along with a `system_id` and password required to access our services.

By default, a maximum of two concurrent connections is permitted per host/system_id combination. If your application requires additional parallel connections, please contact our customer support team for assistance.

### IP Access

Access to the EasySendSMS SMPP servers is restricted to pre-authorized IP addresses. Your client IP range must be provided and added to our firewall for SMPP access.

## Supported SMPP PDUs

| SMPP PDU from Client | SMPP PDU from Server |
| :--- | :--- |
| `bind_transmitter` | `bind_transmitter_resp` |
| `bind_receiver` | `bind_receiver_resp` |
| `bind_transceiver` | `bind_transceiver_resp` |
| `enquire_link` | `enquire_link_resp` |
| `unbind` | `unbind_resp` |
| `submit_sm` | `submit_sm_resp` |
| `data_sm` | `data_sm_resp` |
| `deliver_sm_resp` | `deliver_sm` |
| `generic_nack` | |
| `query_sm` | `query_sm_resp` |
| `cancel_sm` | `cancel_sm_resp` |
| `replace_sm` | `replace_sm_resp` |

## Throughput and Throttling

Throughput refers to the maximum number of mobile-terminated (MT) messages that can be sent per second via the SMPP account on the EasySendSMS server.

> **Default Throughput:** 30 messages per second per bind.
> **To Increase Throughput:** We support throughput up to 500 SMS/Sec; you can contact our support for further details.
> **Recommended Window Size:** 10 (maximum open requests).

Note that the operator receiving the MT messages may have their own capacity limits, which could restrict overall throughput to a specific destination operator. To ensure better distribution across various networks, it is advised to sort destination numbers by the last digits rather than the first.

### Enquire Link
It is recommended to set `enquire_link` requests to a 30-second interval.

### Time Zone
EasySendSMS's SMSC operates on UTC -4:00 (Atlantic Canada).

### MSISDN Format

In GSM, an MSISDN (Mobile Station International Subscriber Directory Number) is structured as follows:

> **MSISDN = CC + NDC + SN**
> **CC:** Country Code
> **NDC:** National Destination Code
> **SN:** Subscriber Number

For more details on MSISDN formatting, refer to the [ITU-T specification E.164](https://www.itu.int/rec/T-REC-E.164).

> ℹ️ **Important Note:**
> If your SMPP system supports only a short username (SMPP v3.4 standard), contact our [Support team](https://www.easysendsms.com/contact-us) to adjust the account username.
> 
> For enhanced security and to comply with certain SMPP systems that require passwords with a maximum of 8 characters, you can set a dedicated SMPP password that differs from your main account password. This can be done in your [account settings](https://my.easysendsms.app/login).

## SMPP Binding

| Description | Value |
| :--- | :--- |
| **Host** | `smpp.easysendsms.com` |
| **Port** | `2777` |
| **Secured Port** | `2778` |
| **Username** | Your account username |
| **Password** | Your account password |
| **Mode** | TX / RX / TRX |
| **Connections** | max 2 connections |
| **Throughput** | 30/Sec. (We support up to 500 SMS/Sec, contact our support for further details). |
| **Dest TON** | Unknown = 0<br>International = 1<br>National = 2<br>Network Specific = 3<br>Subscriber Number = 4<br>Alphanumeric = 5<br>Abbreviated = 6 |
| **DEST NPI** | Unknown = 0<br>ISDN/telephone numbering plan (E163/E164) = 1<br>Data numbering plan (X.121) = 3<br>Telex numbering plan (F.69) = 4<br>Land Mobile (E.212) = 6<br>National numbering plan = 8<br>Private numbering plan = 9<br>ERMES numbering plan (ETSI DE/PS 3 01-3) = 10<br>Internet (IP) = 13<br>WAP Client Id (to be defined by WAP Forum) = 18<br><br>If the sender address is alphanumeric (contains both letters and numbers) or non-numeric, TON is set to 5 and NPI to 0.<br>If the sender address is a short code, TON is set to 3, and NPI is set to 0.<br>If the sender starts with a "+", TON is set to 1, and NPI is set to 1.<br>If the recipient starts with a "+", TON is set to 1, and NPI is set to 1.<br>Otherwise, TON is set to 0 and NPI is set to 1. |

## Delivery Receipt Codes

| Code | Description |
| :--- | :--- |
| **0** | Message sent |
| **1** | Failed message delivery |
| **2** | Message delivered |
| **5** | Failed message delivery |

## SMPP Error Codes

| Hex | Decimal | Description | Possible Solution |
| :--- | :--- | :--- | :--- |
| **0x00000000** | 0 | No Error | - |
| **0x00000001** | 1 | Message length is invalid | Max 140 octets; 160 chars in uncompressed default character encoding. |
| **0x00000002** | 2 | Command length is invalid | - |
| **0x00000003** | 3 | Invalid Command ID | - |
| **0x00000004** | 4 | Incorrect BIND Status for given command | You must bind first before any other request is handled. |
| **0x00000005** | 5 | ESME Already in Bound State | Do not send bind requests when already bound. |
| **0x00000006** | 6 | Invalid Priority Flag | - |
| **0x00000007** | 7 | Invalid Registered Delivery Flag | - |
| **0x00000008** | 8 | System Error | - |
| **0x0000000A** | 10 | Invalid Source Address | - |
| **0x0000000B** | 11 | Invalid Dest Addr | Invalid length; the length was greater than 3 && less than 17, invalid international format. |
| **0x0000000C** | 12 | Message ID is invalid | - |
| **0x0000000D** | 13 | Bind Failed | - |
| **0x0000000E** | 14 | Invalid Password | - |
| **0x0000000F** | 15 | Invalid System ID | - |
| **0x00000010** | 16 | Reserved | - |
| **0x00000011** | 17 | Cancel SM Failed | - |
| **0x00000013** | 19 | Replace SM Failed | - |
| **0x00000014** | 20 | Message Queue Full | - |
| **0x00000015** | 21 | Invalid Service Type | Set to NULL |
| **0x00000033** | 51 | Invalid number of destinations | - |
| **0x00000034** | 52 | Invalid Distribution List name | - |
| **0x00000040** | 64 | Destination flag is invalid (submit_multi) | - |
| **0x00000043** | 67 | Invalid esm_class field data | - |
| **0x00000045** | 69 | submit_sm or submit_multi failed | - |
| **0x00000048** | 72 | Invalid Source address TON | Accepts International, Network, or Alphanumeric; values of 0x01, 0x03, and 0x05. |
| **0x00000049** | 73 | Invalid Source address NPI | Set to null for default value or 0x01 for ISDN numbering plan indicator. |
| **0x00000050** | 80 | Invalid Destination address TON | Accepts either Unknown Or International; values: 0x00 and 0x01. |
| **0x00000051** | 81 | Invalid Destination address NPI | Accepts either Unknown Or ISDN E163/E164: values: 0x00 and 0x01. |
| **0x00000058** | 88 | Throttling error; ESME has exceeded allowed message limits | - |
| **0x00000061** | 97 | Invalid Scheduled Delivery Time | - |
| **0x00000062** | 98 | Invalid message validity period (Expiry time). | - |
| **0x00000063** | 99 | Predefined Message Invalid or Not Found | Does not support canned messages; set to NULL. |
| **0x000000C0** | 192 | Error in the optional part of the PDU Body | - |
| **0x000000C1** | 193 | Optional Parameter not allowed | - |
| **0x000000C2** | 194 | Invalid Parameter Length | - |
| **0x000000C3** | 195 | Expected Optional Parameter missing | - |
| **0x000000C4** | 196 | Invalid Optional Parameter Value | This error occurs when an optional value parameter retrieve fails; this is not normal behavior. |
| **0x000000FE** | 245 | Delivery Failure, used for data_sm_resp | - |
| **0x000000FF** | 255 | Unknown Error | - |
| **0x0000012C** | 300 | Invalid destination address | Number Format Check: Ensure the phone number is in the correct E-164 format. Confirm Phone Number Validity: Ensure that the phone number you are trying to message is valid and currently active. Follow the Rules: Ensure your message meets all the local laws. For Developers: If using SMPP, set TON/NPI values to 1/1. |
| **0x0000012D** | 301 | Invalid destination numbering plan | Permanent |
| **0x0000012E** | 302 | Invalid destination type of number | Permanent |
| **0x0000012F** | 303 | Invalid destination flag | Permanent |
| **0x00000130** | 304 | Invalid number of destinations | Permanent |
| **0x00000136** | 310 | Invalid source address | Check Sender Name/Number: Make sure the sender ID is set up properly. Follow the Rules: Ensure your message meets all the local laws. |
| **0x00000137** | 311 | Invalid source numbering plan | Permanent |
| **0x00000138** | 312 | Invalid source type of number | Permanent |
| **0x00000140** | 320 | ESME Receiver permanent error | Permanent |
| **0x00000141** | 321 | ESME Receiver reject error | Permanent |
| **0x00000142** | 322 | ESME Receiver temporary error | Temporary |
| **0x0000014A** | 330 | Invalid command length | Permanent |
| **0x0000014B** | 331 | Invalid service type | Permanent |
| **0x0000014C** | 332 | Invalid operation | Permanent |
| **0x0000014D** | 333 | Operation not allowed | Permanent |
| **0x0000014E** | 334 | Invalid parameter | Permanent |
| **0x0000014F** | 335 | Parameter not allowed | Permanent |
| **0x00000150** | 336 | Invalid parameter length | Permanent |
| **0x00000151** | 337 | Invalid optional parameter | Permanent |
| **0x00000152** | 338 | Optional parameter missing | Permanent |
| **0x00000153** | 339 | Invalid validity parameter | Permanent |
| **0x00000154** | 340 | Invalid scheduled delivery parameter | Permanent |
| **0x00000155** | 341 | Invalid distribution list | Permanent |
| **0x00000156** | 342 | Invalid message class | Permanent |
| **0x00000157** | 343 | Invalid message length | Permanent |
| **0x00000158** | 344 | Invalid message reference | Permanent |
| **0x00000159** | 345 | Invalid number of messages | Permanent |
| **0x0000015A** | 346 | Invalid predefined message | Permanent |
| **0x0000015B** | 347 | Invalid priority | Permanent |
| **0x0000015C** | 348 | Invalid replace flag | Permanent |
| **0x0000015D** | 349 | Request failed | Permanent |
| **0x0000015E** | 350 | Invalid delivery report request | Temporary |
| **0x00000168** | 360 | Message queue full | Temporary |
| **0x00000169** | 361 | External error | Contact your account manager. Temporary |
| **0x0000016A** | 362 | External error | Contact your account manager. Temporary |
| **0x00000172** | 370 | Can't find information | Temporary |
| **0x0000018F** | 399 | Unknown | Temporary |
| **0x00000406** | 1030 | Invalid data coding scheme | Reserved values used OR unsupported encoding. |
| **0x00000407** | 1031 | Message payload and short message cannot both contain data | Use 1 or the other, invalid message payload content. |
| **0x00000409** | 1033 | Invalid UDH format | Make sure your UDH is correctly formatted. |
| **0x00000411** | 1041 | Deliver_SM not allowed | - |
| **0x00000436** | 1078 | Demo expired | - |
| **0x00000443** | 1091 | Account not enabled for SMPP | - |
| **0xd000** | 53248 | Internal Error | Routing information could not be processed. |
| **0xd001** | 53249 | Customer Blocked | Customer is not allowed to send messages due to account restrictions or network policies. |
| **0xd002** | 53250 | Destination Blocked | The destination network or subscriber is blocked, possibly due to network issues or restrictions. |
| **0xd004** | 53252 | Destination Temporarily Unavailable | The destination is temporarily unavailable due to network or service issues. |
| **0xffff** | 65535 | Internal Error Code | The message delivery failed due to an unspecified internal error. |
| **0xffdd** | 65501 | Destination Blocked | The message could not be delivered because the destination operator is currently not available. |
| **0xfc0a** | 64522 | No Network Response | A network node did not respond within the expected time, leading to message delivery failure. |
