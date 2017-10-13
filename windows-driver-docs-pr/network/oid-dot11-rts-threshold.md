---
title: OID_DOT11_RTS_THRESHOLD
author: windows-driver-content
description: OID\_DOT11\_RTS\_THRESHOLD
ms.assetid: e4049926-7a89-4c32-8789-784dafe76ca3
ms.author: windowsdriverdev
ms.date: 08/08/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
keywords: 
 -OID_DOT11_RTS_THRESHOLD Network Drivers Starting with Windows Vista
---

# OID\_DOT11\_RTS\_THRESHOLD


**Important**  The [Native 802.11 Wireless LAN](https://msdn.microsoft.com/library/windows/hardware/ff560690) interface is deprecated in Windows 10 and later. Please use the WLAN Device Driver Interface (WDI) instead. For more information about WDI, see [WLAN Universal Windows driver model](https://msdn.microsoft.com/library/windows/hardware/dn897672).

 

When set, the OID\_DOT11\_RTS\_THRESHOLD object identifier (OID) requests that the miniport driver set the IEEE 802.11 **dot11RTSThreshold** management information base (MIB) object to the specified value.

When queried, this OID requests that the miniport driver return the value of the **dot11RTSThreshold** MIB object.

The **dot11RTSThreshold** MIB object specifies the maximum length that a MAC protocol data unit (MPDU) frame can have before the 802.11 station initiates the 802.11 request to send (RTS)/clear to send (CTS) handshake. For more information about the RTS/CTS handshake and RTS threshold, refer to Clause 9.3 of the IEEE 802.11-2012 standard.

The data type for OID\_DOT11\_RTS\_THRESHOLD is a ULONG value that specifies the RTS threshold in bytes.

The value of the **dot11RTSThreshold** MIB object must be from 0 through 2347.

When OID\_DOT11\_RTS\_THRESHOLD is set, the following actions apply to the 802.11 station:

-   The 802.11 station must use the new RTS threshold value on all MAC service data unit (MSDU) packets passed after the set request by the operating system to the miniport driver's [*MiniportSendNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff559440) function.

-   The 802.11 station can use the new RTS threshold value on all MSDU packets that are pending in the station's transmit queue. Alternatively, the 802.11 station can continue to use the old RTS threshold value for the pending MSDU packets.

-   The 802.11 station must not use the new RTS threshold value for any MPDU frames of the MSDU packet that the station is transmitting when OID\_DOT11\_RTS\_THRESHOLD is set.

The default value for the **dot11RTSThreshold** MIB object is 2347. The miniport driver must set this MIB object to its default when one of the following occurs:

-   The miniport driver's [*MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389) function is called.

-   A method request of [OID\_DOT11\_RESET\_REQUEST](oid-dot11-reset-request.md) is made to reset the MAC layer of the 802.11 station and the **bSetDefaultMIB** member of the DOT11\_RESET\_REQUEST structure is **TRUE**.

**Note**  A Native 802.11 miniport driver that is designed to run on the Windows Vista or Windows Server 2008 operating systems must always reset this 802.11 MIB OID to its default value. This is the case regardless of the value of the **bSetDefaultMIB** member of the DOT11\_RESET\_REQUEST structure. This requirement applies to a miniport driver that, in a call to the **NdisMSetMiniportAttributes** function, sets **MiniportAttributes** -&gt; **Native\_802\_11\_Attributes** -&gt; **Header** -&gt; **Revision** to NDIS\_MINIPORT\_ADAPTER\_802\_11\_ATTRIBUTES\_REVISION\_1.

 

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>Available in Windows Vista and later versions of the Windows operating systems.</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Windot11.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## See also


[Native 802.11 MIB OIDs](https://msdn.microsoft.com/library/windows/hardware/ff560645)

[Native 802.11 Wireless LAN OIDs](https://msdn.microsoft.com/library/windows/hardware/ff560691)

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bnetvista\netvista%5D:%20OID_DOT11_RTS_THRESHOLD%20%20RELEASE:%20%288/8/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")

