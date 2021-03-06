---
title: "SMS_StatAttr Class | Microsoft Docs"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 954660ad-f047-4944-90a2-e50f91d1861e
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_StatAttr Server WMI Class
The `SMS_StatAttr` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a high-performance version of [SMS_StatMsgAttributes Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statmsgattributes-server-wmi-class.md).  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_StatAttr : SMS_BaseClass  
{  
      UInt32 AttributeID;  
      DateTime AttributeTime;  
      String AttributeValue;  
      SInt64 RecordID;  
};  
```  

## Methods  
 The `SMS_StatAttr` class does not define any methods.  

## Properties  
 `AttributeID`  
 Data type: `UInt32`  

 Access type: Read  

 Qualifiers:  

 [key]  

 ID of the type of attribute that is defined by the `AttributeValue` property. See the `AttributeID` property of [SMS_StatMsgAttributes Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statmsgattributes-server-wmi-class.md).  

 `AttributeTime`  
 Data type: `DateTime`  

 Access type: Read  

 Qualifiers: [none]  

 Date and time, in Universal Coordinated Time (UTC), when the message was generated.  

 `AttributeValue`  
 Data type: `String`  

 Access type: Read  

 Qualifiers: [none]  

 Attribute value that is determined by the type indicated by the `AttributeID` property.  

 `RecordID`  
 Data type: `SInt64`  

 Access type: Read  

 Qualifiers: none  

 Record ID of the status message with which the attribute is associated.  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 Use this class to associate specific information with a message. The attribute data is not displayed in the message text. Typically, the attribute values are used to query for status messages that reference a particular object. For example, your application can query for the attribute that retrieves all the messages associated with a particular Configuration Manager package.  

 Each attribute is stored as an instance of this class. Your application can use the raise status message methods to add attribute values. To delete attribute values, the application deletes the associated status message.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Status Server WMI Classes](../../../../../develop/reference/core/servers/manage/status-server-wmi-classes.md)   
 [SMS_StatMsgAttributes Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statmsgattributes-server-wmi-class.md)
