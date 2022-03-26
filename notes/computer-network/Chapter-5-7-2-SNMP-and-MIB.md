## The Simple Network Management Protocol (SNMP) and the Management Information Base (MIB)

### SNMP 
- SNMPv3 is an application-layer protocol
- used to convey network-management control and information messages between managing server and agent.

> the most common usage of SNMP is in a request-response model
> an SNMP server sends a request to an SNMP agent
> the agent receive the request, performs some action, and sends a reply to the request.
> a request will be used to query(retrieve) or modify MIB object values associated with a managed device.

> a second common usage of SNMP is for an agent to send an unsolicited message known as a **trap message** to a managing server.
> trap message are used to notify a managing server of an exceptional situation (e.g.,link interface going up or down)
> that has resulted in changes to MIB object values.

### MIB
- MIB objects are specified in a data desscription language known as **SMI** Structure of Management Information
- a formal definition language is used to ensure that the syntax and semantics of the network management data are well defined and unambiguous.
- related MIB objects are gathered into MIB modules.

### PDU (protocol data units) 协议数据单元
- SNMPv3 defines seven types of messages, known as PDU (protocol data units)

| SNMPv3 PDU Type  | Sender-receiver | Description  |
|:--|:--|:--|
|GetRequest   | manager-to-agent  | get value of one or more MIB objects instances  |
|GetNextRequest   | manager-to-agent  |get value of next MIB object instances in list or table   |
|GetBulkRequest   | manager-to-agent  |get values in large block of data, e.g. values in a large table   |
|InformRequest   | manager-to-manager  |inform remote managing entity of MIB values remote to its access   |
|SetRequest   |manager-to-agent   |set value of one or more MIB object instances   |
|Response   |agent-to-manager or manager-to-manager   | generated in response  |
|SNMP Trap | agent-to-manager |inform manager of an exceptional event |
