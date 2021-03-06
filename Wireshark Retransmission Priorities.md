| TCP Keep-Alive | TCP Spurious Retransmission [^1] | TCP Fast Retransmission | TCP Out-Of-Order | TCP Retransmission |
| --- | --- | --- | --- | --- |
| The segment size is zero or one | This is not a keepalive packet. | This is not a keepalive packet. | This is not a keepalive packet. | This is not a keepalive packet. |
| "The current sequence number is one byte less than the next expected sequence number<br>Or SYN, FIN, or RST flags are set." | "The segment length is greater than zero<br>or The SYN or FIN flag is set." | "In the forward direction, the segment size is greater than zero<br>or the SYN or FIN is set." | "In the forward direction, the segment length is greater than zero<br>or the SYN or FIN flag is set." | "In the forward direction[^2], the segment length is greater than zero<br>or the SYN or FIN flag is set." |
|     | Data for this flow has been acknowledged. That is, the last-seen acknowledgement number has been set. | The next expected sequence number is greater than the current sequence number. | The next expected sequence number is greater than the current sequence number. | The next expected sequence number is greater than the current sequence number. |
|     | The next sequence number is less than or equal to the last-seen acknowledgement number. | We have more than two duplicate ACKs in the reverse direction. | The next expected sequence number and the next sequence number differ. |     |
|     |     | The current sequence number equals the next expected acknowledgement number. | "The last segment arrived within the Out-Of-Order RTT threshold. The threshold is either the value shown in the “iRTT” (tcp.analysis.initial_rtt) field under “SEQ/ACK analysis” if it is present.<br>If not present, the default value of 3ms is used.**" |     |
|     | Note: If the ACK didn't make it to the server, this isn't really a Spurious Retransmission - it's just a standard Retransmission. On the sender side, Wireshark must mark it as a Spurious Retransmission because the ACK was seen in the trace | We saw the last acknowledgement less than 20ms ago. |     |     |
| "Supersedes<br>TCP Fast Retransmission, TCP Out-Of-Order,<br>TCP Spurious Retransmission and<br>TCP Retransmission" | "Supersedes<br>TCP Fast Retransmission,<br>TCP Out-Of-Order and<br>TCP Retransmission" | "Supersedes<br>TCP Out-Of-Order and<br>TCP Retransmission" | "Supersedes TCP Retransmission" |     |

[^1]: Checks for a retransmission based on analysis data in the reverse direction[^3].

[^2]: Forward Direction - Direction of data transfer, sender to receiver

[^3]: Reverse Direction - Direction of Acks for the data, receiver to sender