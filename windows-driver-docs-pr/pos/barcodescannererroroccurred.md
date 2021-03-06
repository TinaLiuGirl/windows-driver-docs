---
title: BarcodeScannerErrorOccurred
description: The BarcodeScannerErrorOccurred event occurs when there is an error, such as a scanning error.
ms.assetid: '38cfbd87-0526-49d1-8580-96f4e1adf7bb'
ms.author: windowsdriverdev
ms.date: 9/7/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
---

# BarcodeScannerErrorOccurred

This event occurs when there is an error, such as a scanning error.

The data buffer for this event is as follows.

## Syntax

``` syntax
// Error occurred data should fill the ReadFile buffer in this order:
//    PosBarcodeScannerErrorOccurredEventData structure (length = sizeof(PosBarcodeScannerErrorOccurredEventData))
//    Error Message (length = MessageLength)
//    Scan Data (length = ScanDataLength)
//    Scan Data Label (length = ScanDataLabelLength)

typedef struct _PosBarcodeScannerErrorOccurredEventData
{
    PosEventDataHeader Header;
    LONG IsRetriable;
    UnifiedPosErrorSeverity Severity;
    UINT32 VendorErrorCode;
    UnifiedPosErrorReason Reason;
    UINT32 ExtendedReason;
    UINT32 MessageLength;
    PosBarcodeScannerDataReceivedEventData PartialData;
} PosBarcodeScannerErrorOccurredEventData;
```

The following table shows the memory layout of the data buffer for this event.

| Memory value                                      | Description                                                                                                                                        |
|---------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| 0x00000006                             | **EventType = PosEventType:: BarcodeScannerTriggerPressed**                                                                             |
| UINT32                                 | **DataLength** = sizeof(**PosBarcodeScannerErrorOccurredData**) + **MessageLength** + **ScanDataLength** + **ScanDataLabelLength**)     |
| BOOL                                   | **IsRetriable**                                                                                                                         |
| 32-bit UnifiedPosErrorSeverity         | **Severity**                                                                                                                            |
| UINT32                                 | **VendorErrorCode**                                                                                                                     |
| 32-bit UnifiedPosErrorReason           | **Reason**                                                                                                                              |
| UINT32                                 | **ExtendedReason**                                                                                                                      |
| UINT32                                 | **MessageLength**                                                                                                                       |
| PosBarcodeScannerDataReceivedEventData | **PartialData**                                                                                                                         |
| UINT32                                 | **EventType** not specified                                                                                                             |
| UINT32                                 | **DataLength** = sizeof(**PosBarcodeScannerDataRecievedEventData**) + **MessageLength** + **ScanDataLength** + **ScanDataLabelLength**) |
| UINT32                                 | **DataType** not specified                                                                                                              |
| UINT32                                 | **ScanDataLength**                                                                                                                      |
| UINT32                                 | **ScanDataLabelLength**                                                                                                                 |
| byte \[\]                              | **MessageLength** bytes of message                                                                                                      |
| byte \[\]                              | **ScanDataLength** bytes of label data                                                                                                  |
| byte \[\]                              | **ScanDataLabelLength** bytes of scan data                                                                                              |



## Remarks

If a scanning error occurs, and some scan data was obtained, the event data contains the partial scan data.

## Requirements

**Header:** pointofservicedriverinterface.h
