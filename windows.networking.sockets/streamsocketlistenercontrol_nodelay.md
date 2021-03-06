---
-api-id: P:Windows.Networking.Sockets.StreamSocketListenerControl.NoDelay
-api-type: winrt property
---

<!-- Property syntax
public bool NoDelay { get;  set; }
-->

# Windows.Networking.Sockets.StreamSocketListenerControl.NoDelay

## -description
A value that indicates whether the Nagle algorithm is used on a [StreamSocket](streamsocket.md) object created when a connection is received by the [StreamSocketListener](streamsocketlistener.md) object.

## -property-value
A value that indicates whether the Nagle algorithm is used on the TCP connection of a [StreamSocket](streamsocket.md) object created.

## -remarks
The [NoDelay](streamsocketlistenercontrol_nodelay.md) property controls whether Nagle's algorithm is enabled or disabled on a [StreamSocket](streamsocket.md) object created. The default value for the [NoDelay](streamsocketcontrol_nodelay.md) property on a [StreamSocket](streamsocket.md) is **true**.

Nagle's algorithm is a technique to improving the efficiency of TCP/IP networks by reducing the number of packets that are needed to be sent over the network. The algorithm tries to deal with problems caused by an application that repeatedly emits data in small chunks. A TCP packet has a 40-byte header (20 bytes for IP and 20 bytes for TCP). So if an app sends only 4 bytes in a packet, the overhead on the packet data is very large. This can occur for a remote access protocol (telnet or secure shell, for example) where most key presses may generate only a single byte or two of data that is transmitted immediately. Over a slow link, many of these packets may be in transit over the network at the same time. Nagle's algorithm works by combining a number of small outgoing messages, and sending them all at once. When there is a sent packet for which the sender has received no acknowledgment, the sender keeps buffering output until it has a full packet's worth of output. This allows the output to be sent all at once. The impact of applying Nagle's algorithm is to increase the bandwidth at the expense of latency. A well-written app that buffers sends internally should not need to use Nagle's algorithm.

When this property is **true**, the [StreamSocket](streamsocket.md) will disable Nagle's algorithm on the TCP connection. This setting reduces the potential delays when sending small messages. When a [StreamSocket](streamsocket.md) is created, the default value for this property is **true**.

When this property is **false**, the [StreamSocket](streamsocket.md) will enable Nagle's algorithm on the TCP connection. This setting can increase the bandwidth at the expense of latency, but should only be used with caution. There are some adverse side effects possible when Nagle's algorithm is enabled and certain other TCP optimizations are also used.

This property may be set before the [StreamSocketListener](streamsocketlistener.md) starts listening for incoming connections. After the [StreamSocketListener](streamsocketlistener.md) starts listening for incoming connections, setting the property will result in an error.

This property sets the value of the **TCP_NODELAY** socket option on the TCP socket used by the [StreamSocket](streamsocket.md).

## -examples

## -see-also
[How to use advanced socket controls ](http://msdn.microsoft.com/library/2e1071d8-a1c7-44c0-b93a-31a701d431c4), [How to use advanced socket controls ](http://msdn.microsoft.com/library/f2c5be73-3461-452e-a38f-d2ddef9b5682), [StreamSocket](streamsocket.md), [StreamSocketListener](streamsocketlistener.md)