# IEC standards for Fieldbus and Real Time Ethernet

In Industrial Automation, all networking protocols live inside the [IEC 61158](https://en.wikipedia.org/wiki/Fieldbus#IEC_61158_specification) standard specification known as: [Fieldbus](http://www.fieldbus.org/index.html). These protocols are specific Factory Autmation and target Real Time requirements.

Ethernet is not part of Fieldbus and share nothing with it. However, its utilizations in Industrial Automation are today part of a separate standard (the RTE standard) which is related to IEC 61158.

## IEC 61158
Fieldbus is not easy to explain as it consists of different sets of protocols. Given the many different requirements in automation, manufacturers have moved on their own by developing many different protocols, each for a specific requirement, and all the efforts made by the community to define a unified standard failed.

However an attempt to organize and provide order in the moltitude of protocols has been made and its final results are collected in IEC 61158, a document which structures the different automation protocols defined in the context of Fieldbus and its applications.

### Protocol sets
The document defines 8 different protocol sets (referrede to as: _types_) which are the basic networking technologies which can be used in Automation. 3 of the most important are:

| Type | Name |
|:----:|:-----|
| Type 1 | [Foundation Fieldbus](https://en.wikipedia.org/wiki/Foundation_Fieldbus_H1) |
| Type 3 | [Profibus](https://en.wikipedia.org/wiki/Profibus) |
| Type 7 | [World-FIP](https://en.wikipedia.org/wiki/Factory_Instrumentation_Protocol) |

Each one of them typically developed by a different manufacturer.

### Standard structure
The IEC 61158 standard specification is a document structured into 7 different sections. Among all of them, we can find up to 16 different networks being described (those come up as part of IEC 61784):

| Section | Title |
|:-------:|:------|
| IEC 61158-1 | Overview and guidance for the IEC 61158 series |
| IEC 61158-2 | Physical Layer specification and service definition |
| IEC 61158-3 | Data Link Service definition |
| IEC 61158-4 | Data Link Protocol specification |
| IEC 61158-5 | Application Layer Service definition |
| IEC 61158-6 | Application Layer Protocol specification |
| IEC 61158-7 | Network management |

## IEC 61784
As we mentioned before, Ethernet is not part of the Fieldbus specification, however a standard has been created, related to IEC 61158, which provides guidelines for using Ethernet in automation environments. This standard is IEC 61784, referred to as: _Real Time Ethernet_.

> IEC 61784 defines protocols for RT networking using Fieldbus, Ethernet and IEEE 802.3.

**Relation to IEC 61158** The standard basically refers to IEC 61158 and all its protocol sets in order to define up to 16 different protocol stacks (communication profile) which can be used in Automation. 

> We can safely state that IEC 61784 shows up the 16 possible combinations of IEC 61158 types which can create a usable network targeting specific requirements.

### Standard structure
The document is organized into 5 sections, the most important for us are:

| Section | Description |
|:-------:|:------|
| IEC 61784-1 | CPs for continuos and discrete manufacturing on Fieldbus |
| IEC 61784-2 | Additional CPs for 802.3 utilization in manufacturing |

**Communication Profile** The standard introduces the concept of _Communication Profile_ as a set of IEC 61158 protocols which can be composed together in order to create a network targeting specific requirements. Each CP uses protocols defined in IEC 61158:

- Physical protocols are taken from IEC 61158-2
- DLL protocols are taken from IEC 61158-3 and IEC 61158-4
- AL protocols are taken from IEC 61158-5 and IEC 61158-6 

### Communication Profile Families 
Since CPs can be many, they are all organized into families (following manufacturer). 16 different families originate, among the most important we find:

| CPF | Based on | Brand name |
|:---:|:--------:|:----------:|
| CPF-3 | Fieldbus | Profibus |
| CPF-5 | Fieldbus | World-FIP |
| CPF-13 | Ethernet 802.3 | Ethernet PowerLink |
| CPF-15 | Ethernet 802.3 | Modbus |
| CPF-16 | Ethernet 802.3 | SERCOS |

Families like Profibus and World-FIP are defined in IEC 61784-1, while all those specific to IEEE 802.3, like Ethernet PowerLink or Modbus, are defined in IEC 61784-2.