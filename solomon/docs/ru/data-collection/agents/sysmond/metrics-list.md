# Список метрик собираемых sysmond

В данном разделе описаны метрики, которые собирает [sysmond](./overview.md).

<small>Таблица 1 — Список метрик собираемых sysmond</small>

Имя метрики | Единица измерения | Метки | Описание
------------|-------------------|-------|---------
/Cpu/PhysicalCpuFrequency/Avg | Герцы | `PhysicalCpuId` |
/Cpu/PhysicalCpuFrequency/Max | Герцы | `PhysicalCpuId` |
/Cpu/PhysicalCpuFrequency/Min | Герцы | `PhysicalCpuId` |

Имя метрики | Единица измерения | Метки | Описание
------------|-------------------|-------|---------
/Io/Disks/IOMillisec | | `disk` |
/Io/Disks/IOServiceTime | | `disk` |
/Io/Disks/IOsInProgress | | `disk` |
/Io/Disks/ReadBytes | | `disk` |
/Io/Disks/ReadWaitMillisec | | `disk` |
/Io/Disks/ReadWaitMillisecAvg | | `disk` |
/Io/Disks/Reads | | `disk` |
/Io/Disks/TimeInQueueMillisec | | `disk` |
/Io/Disks/WriteBytes | | `disk` |
/Io/Disks/WriteWaitMillisec | | `disk` |
/Io/Disks/WriteWaitMillisecAvg | | `disk` |
/Io/Disks/Writes | | `disk` |

Имя метрики | Единица измерения | Метки | Описание
------------|-------------------|-------|---------
/Memory/Active | | |
/Memory/ActiveAnon | | |
/Memory/ActiveFile | | |
/Memory/AnonHugePages | | |
/Memory/AnonPages | | |
/Memory/Buffers | | |
/Memory/Cached | | |
/Memory/CommitLimit | | |
/Memory/Committed_AS | | |
/Memory/Dirty | | |
/Memory/Inactive | | |
/Memory/InactiveAnon | | |
/Memory/InactiveFile | | |
/Memory/MajorPageFaults | | |
/Memory/Mapped | | |
/Memory/MemAvailable | | |
/Memory/MemFree | | |
/Memory/MemTotal | | |
/Memory/Mlocked | | |
/Memory/PageIns | | |
/Memory/PageOuts | | |
/Memory/PageTables | | |
/Memory/Shmem | | |
/Memory/Slab | | |
/Memory/SwapCached | | |
/Memory/SwapFree | | |
/Memory/SwapIns | | |
/Memory/SwapOuts | | |
/Memory/SwapTotal | | |
/Memory/Unevictable | | |
/Memory/Writeback | | |

Имя метрики | Единица измерения | Метки | Описание
------------|-------------------|-------|---------
/Net/Ifs/RxBytes | | `intf` |
/Net/Ifs/RxDrop | | `intf` |
/Net/Ifs/RxErrs | | `intf` |
/Net/Ifs/RxPackets | | `intf` |
/Net/Ifs/TxBytes | | `intf` |
/Net/Ifs/TxDrop | | `intf` |
/Net/Ifs/TxErrs | | `intf` |
/Net/Ifs/TxPackets | | `intf` |

Имя метрики | Единица измерения | Метки | Описание
------------|-------------------|-------|---------
/Net/Netstat/IpExt/InBcastOctets | | |
/Net/Netstat/IpExt/InBcastPkts | | |
/Net/Netstat/IpExt/InCEPkts | | |
/Net/Netstat/IpExt/InCsumErrors | | |
/Net/Netstat/IpExt/InECT0Pkts | | |
/Net/Netstat/IpExt/InECT1Pkts | | |
/Net/Netstat/IpExt/InMcastOctets | | |
/Net/Netstat/IpExt/InMcastPkts | | |
/Net/Netstat/IpExt/InNoECTPkts | | |
/Net/Netstat/IpExt/InNoRoutes | | |
/Net/Netstat/IpExt/InOctets | | |
/Net/Netstat/IpExt/InTruncatedPkts | | |
/Net/Netstat/IpExt/OutBcastOctets | | |
/Net/Netstat/IpExt/OutBcastPkts | | |
/Net/Netstat/IpExt/OutMcastOctets | | |
/Net/Netstat/IpExt/OutMcastPkts | | |
/Net/Netstat/IpExt/OutOctets | | |
/Net/Netstat/TcpExt/ArpFilter | | |
/Net/Netstat/TcpExt/BusyPollRxPackets | | |
/Net/Netstat/TcpExt/DelayedACKLocked | | |
/Net/Netstat/TcpExt/DelayedACKLost | | |
/Net/Netstat/TcpExt/DelayedACKs | | |
/Net/Netstat/TcpExt/EmbryonicRsts | | |
/Net/Netstat/TcpExt/IPReversePathFilter | | |
/Net/Netstat/TcpExt/ListenDrops | | |
/Net/Netstat/TcpExt/ListenOverflows | | |
/Net/Netstat/TcpExt/LockDroppedIcmps | | |
/Net/Netstat/TcpExt/OfoPruned | | |
/Net/Netstat/TcpExt/OutOfWindowIcmps | | |
/Net/Netstat/TcpExt/PAWSActive | | |
/Net/Netstat/TcpExt/PAWSEstab | | |
/Net/Netstat/TcpExt/PruneCalled | | |
/Net/Netstat/TcpExt/RcvPruned | | |
/Net/Netstat/TcpExt/SyncookiesFailed | | |
/Net/Netstat/TcpExt/SyncookiesRecv | | |
/Net/Netstat/TcpExt/SyncookiesSent | | |
/Net/Netstat/TcpExt/TCPACKSkippedChallenge | | |
/Net/Netstat/TcpExt/TCPACKSkippedFinWait2 | | |
/Net/Netstat/TcpExt/TCPACKSkippedPAWS | | |
/Net/Netstat/TcpExt/TCPACKSkippedSeq | | |
/Net/Netstat/TcpExt/TCPACKSkippedSynRecv | | |
/Net/Netstat/TcpExt/TCPACKSkippedTimeWait | | |
/Net/Netstat/TcpExt/TCPAbortFailed | | |
/Net/Netstat/TcpExt/TCPAbortOnClose | | |
/Net/Netstat/TcpExt/TCPAbortOnData | | |
/Net/Netstat/TcpExt/TCPAbortOnLinger | | |
/Net/Netstat/TcpExt/TCPAbortOnMemory | | |
/Net/Netstat/TcpExt/TCPAbortOnTimeout | | |
/Net/Netstat/TcpExt/TCPAutoCorking | | |
/Net/Netstat/TcpExt/TCPBacklogDrop | | |
/Net/Netstat/TcpExt/TCPChallengeACK | | |
/Net/Netstat/TcpExt/TCPDSACKIgnoredNoUndo | | |
/Net/Netstat/TcpExt/TCPDSACKIgnoredOld | | |
/Net/Netstat/TcpExt/TCPDSACKOfoRecv | | |
/Net/Netstat/TcpExt/TCPDSACKOfoSent | | |
/Net/Netstat/TcpExt/TCPDSACKOldSent | | |
/Net/Netstat/TcpExt/TCPDSACKRecv | | |
/Net/Netstat/TcpExt/TCPDSACKUndo | | |
/Net/Netstat/TcpExt/TCPDeferAcceptDrop | | |
/Net/Netstat/TcpExt/TCPFastOpenActive | | |
/Net/Netstat/TcpExt/TCPFastOpenActiveFail | | |
/Net/Netstat/TcpExt/TCPFastOpenCookieReqd | | |
/Net/Netstat/TcpExt/TCPFastOpenListenOverflow | | |
/Net/Netstat/TcpExt/TCPFastOpenPassive | | |
/Net/Netstat/TcpExt/TCPFastOpenPassiveFail | | |
/Net/Netstat/TcpExt/TCPFastRetrans | | |
/Net/Netstat/TcpExt/TCPFromZeroWindowAdv | | |
/Net/Netstat/TcpExt/TCPFullUndo | | |
/Net/Netstat/TcpExt/TCPHPAcks | | |
/Net/Netstat/TcpExt/TCPHPHits | | |
/Net/Netstat/TcpExt/TCPHystartDelayCwnd | | |
/Net/Netstat/TcpExt/TCPHystartDelayDetect | | |
/Net/Netstat/TcpExt/TCPHystartTrainCwnd | | |
/Net/Netstat/TcpExt/TCPHystartTrainDetect | | |
/Net/Netstat/TcpExt/TCPKeepAlive | | |
/Net/Netstat/TcpExt/TCPLossFailures | | |
/Net/Netstat/TcpExt/TCPLossProbeRecovery | | |
/Net/Netstat/TcpExt/TCPLossProbes | | |
/Net/Netstat/TcpExt/TCPLossUndo | | |
/Net/Netstat/TcpExt/TCPLostRetransmit | | |
/Net/Netstat/TcpExt/TCPMD5NotFound | | |
/Net/Netstat/TcpExt/TCPMD5Unexpected | | |
/Net/Netstat/TcpExt/TCPMTUPFail | | |
/Net/Netstat/TcpExt/TCPMTUPSuccess | | |
/Net/Netstat/TcpExt/TCPMemoryPressures | | |
/Net/Netstat/TcpExt/TCPMinTTLDrop | | |
/Net/Netstat/TcpExt/TCPOFODrop | | |
/Net/Netstat/TcpExt/TCPOFOMerge | | |
/Net/Netstat/TcpExt/TCPOFOQueue | | |
/Net/Netstat/TcpExt/TCPOrigDataSent | | |
/Net/Netstat/TcpExt/TCPPartialUndo | | |
/Net/Netstat/TcpExt/TCPPureAcks | | |
/Net/Netstat/TcpExt/TCPRcvCoalesce | | |
/Net/Netstat/TcpExt/TCPRcvCollapsed | | |
/Net/Netstat/TcpExt/TCPRenoFailures | | |
/Net/Netstat/TcpExt/TCPRenoRecovery | | |
/Net/Netstat/TcpExt/TCPRenoRecoveryFail | | |
/Net/Netstat/TcpExt/TCPRenoReorder | | |
/Net/Netstat/TcpExt/TCPReqQFullDoCookies | | |
/Net/Netstat/TcpExt/TCPReqQFullDrop | | |
/Net/Netstat/TcpExt/TCPRetransFail | | |
/Net/Netstat/TcpExt/TCPSACKDiscard | | |
/Net/Netstat/TcpExt/TCPSACKReneging | | |
/Net/Netstat/TcpExt/TCPSACKReorder | | |
/Net/Netstat/TcpExt/TCPSYNChallenge | | |
/Net/Netstat/TcpExt/TCPSackFailures | | |
/Net/Netstat/TcpExt/TCPSackMerged | | |
/Net/Netstat/TcpExt/TCPSackRecovery | | |
/Net/Netstat/TcpExt/TCPSackRecoveryFail | | |
/Net/Netstat/TcpExt/TCPSackShiftFallback | | |
/Net/Netstat/TcpExt/TCPSackShifted | | |
/Net/Netstat/TcpExt/TCPSlowStartRetrans | | |
/Net/Netstat/TcpExt/TCPSpuriousRTOs | | |
/Net/Netstat/TcpExt/TCPSpuriousRtxHostQueues | | |
/Net/Netstat/TcpExt/TCPSynRetrans | | |
/Net/Netstat/TcpExt/TCPTSReorder | | |
/Net/Netstat/TcpExt/TCPTimeWaitOverflow | | |
/Net/Netstat/TcpExt/TCPTimeouts | | |
/Net/Netstat/TcpExt/TCPToZeroWindowAdv | | |
/Net/Netstat/TcpExt/TCPWantZeroWindowAdv | | |
/Net/Netstat/TcpExt/TCPWinProbe | | |
/Net/Netstat/TcpExt/TW | | |
/Net/Netstat/TcpExt/TWKilled | | |
/Net/Netstat/TcpExt/TWRecycled | | |

Имя метрики | Единица измерения | Метки | Описание
------------|-------------------|-------|---------
/Net/ProtocolSocketState/alloc | | `Protocol` |
/Net/ProtocolSocketState/inuse | | `Protocol` |
/Net/ProtocolSocketState/mem | | `Protocol` |
/Net/ProtocolSocketState/memory | | `Protocol` |
/Net/ProtocolSocketState/orphan | | `Protocol` |
/Net/ProtocolSocketState/tw | | `Protocol` |

Имя метрики | Единица измерения | Метки | Описание
------------|-------------------|-------|---------
/Net/Snmp/Icmp/InAddrMaskReps
/Net/Snmp/Icmp/InAddrMasks
/Net/Snmp/Icmp/InCsumErrors
/Net/Snmp/Icmp/InDestUnreachs
/Net/Snmp/Icmp/InEchoReps
/Net/Snmp/Icmp/InEchos
/Net/Snmp/Icmp/InErrors
/Net/Snmp/Icmp/InMsgs
/Net/Snmp/Icmp/InParmProbs
/Net/Snmp/Icmp/InRedirects
/Net/Snmp/Icmp/InSrcQuenchs
/Net/Snmp/Icmp/InTimeExcds
/Net/Snmp/Icmp/InTimestampReps
/Net/Snmp/Icmp/InTimestamps
/Net/Snmp/Icmp/OutAddrMaskReps
/Net/Snmp/Icmp/OutAddrMasks
/Net/Snmp/Icmp/OutDestUnreachs
/Net/Snmp/Icmp/OutEchoReps
/Net/Snmp/Icmp/OutEchos
/Net/Snmp/Icmp/OutErrors
/Net/Snmp/Icmp/OutMsgs
/Net/Snmp/Icmp/OutParmProbs
/Net/Snmp/Icmp/OutRedirects
/Net/Snmp/Icmp/OutSrcQuenchs
/Net/Snmp/Icmp/OutTimeExcds
/Net/Snmp/Icmp/OutTimestampReps
/Net/Snmp/Icmp/OutTimestamps
/Net/Snmp/IcmpMsg/InType3
/Net/Snmp/IcmpMsg/OutType3
/Net/Snmp/Ip/DefaultTTL
/Net/Snmp/Ip/ForwDatagrams
/Net/Snmp/Ip/Forwarding
/Net/Snmp/Ip/FragCreates
/Net/Snmp/Ip/FragFails
/Net/Snmp/Ip/FragOKs
/Net/Snmp/Ip/InAddrErrors
/Net/Snmp/Ip/InDelivers
/Net/Snmp/Ip/InDiscards
/Net/Snmp/Ip/InHdrErrors
/Net/Snmp/Ip/InReceives
/Net/Snmp/Ip/InUnknownProtos
/Net/Snmp/Ip/OutDiscards
/Net/Snmp/Ip/OutNoRoutes
/Net/Snmp/Ip/OutRequests
/Net/Snmp/Ip/ReasmFails
/Net/Snmp/Ip/ReasmOKs
/Net/Snmp/Ip/ReasmReqds
/Net/Snmp/Ip/ReasmTimeout
/Net/Snmp/Tcp/ActiveOpens
/Net/Snmp/Tcp/AttemptFails
/Net/Snmp/Tcp/CurrEstab
/Net/Snmp/Tcp/EstabResets
/Net/Snmp/Tcp/InCsumErrors
/Net/Snmp/Tcp/InErrs
/Net/Snmp/Tcp/InSegs
/Net/Snmp/Tcp/MaxConn
/Net/Snmp/Tcp/OutRsts
/Net/Snmp/Tcp/OutSegs
/Net/Snmp/Tcp/PassiveOpens
/Net/Snmp/Tcp/RetransSegs
/Net/Snmp/Tcp/RtoAlgorithm
/Net/Snmp/Tcp/RtoMax
/Net/Snmp/Tcp/RtoMin
/Net/Snmp/Udp/IgnoredMulti
/Net/Snmp/Udp/InCsumErrors
/Net/Snmp/Udp/InDatagrams
/Net/Snmp/Udp/InErrors
/Net/Snmp/Udp/NoPorts
/Net/Snmp/Udp/OutDatagrams
/Net/Snmp/Udp/RcvbufErrors
/Net/Snmp/Udp/SndbufErrors
/Net/Snmp/UdpLite/IgnoredMulti
/Net/Snmp/UdpLite/InCsumErrors
/Net/Snmp/UdpLite/InDatagrams
/Net/Snmp/UdpLite/InErrors
/Net/Snmp/UdpLite/NoPorts
/Net/Snmp/UdpLite/OutDatagrams
/Net/Snmp/UdpLite/RcvbufErrors
/Net/Snmp/UdpLite/SndbufErrors
/Net/Snmp6/Icmp6InCsumErrors
/Net/Snmp6/Icmp6InDestUnreachs
/Net/Snmp6/Icmp6InEchoReplies
/Net/Snmp6/Icmp6InEchos
/Net/Snmp6/Icmp6InErrors
/Net/Snmp6/Icmp6InGroupMembQueries
/Net/Snmp6/Icmp6InGroupMembReductions
/Net/Snmp6/Icmp6InGroupMembResponses
/Net/Snmp6/Icmp6InMLDv2Reports
/Net/Snmp6/Icmp6InMsgs
/Net/Snmp6/Icmp6InNeighborAdvertisements
/Net/Snmp6/Icmp6InNeighborSolicits
/Net/Snmp6/Icmp6InParmProblems
/Net/Snmp6/Icmp6InPktTooBigs
/Net/Snmp6/Icmp6InRedirects
/Net/Snmp6/Icmp6InRouterAdvertisements
/Net/Snmp6/Icmp6InRouterSolicits
/Net/Snmp6/Icmp6InTimeExcds
/Net/Snmp6/Icmp6InType1
/Net/Snmp6/Icmp6InType2
/Net/Snmp6/Icmp6InType3
/Net/Snmp6/Icmp6InType128
/Net/Snmp6/Icmp6InType135
/Net/Snmp6/Icmp6InType136
/Net/Snmp6/Icmp6OutDestUnreachs
/Net/Snmp6/Icmp6OutEchoReplies
/Net/Snmp6/Icmp6OutEchos
/Net/Snmp6/Icmp6OutErrors
/Net/Snmp6/Icmp6OutGroupMembQueries
/Net/Snmp6/Icmp6OutGroupMembReductions
/Net/Snmp6/Icmp6OutGroupMembResponses
/Net/Snmp6/Icmp6OutMLDv2Reports
/Net/Snmp6/Icmp6OutMsgs
/Net/Snmp6/Icmp6OutNeighborAdvertisements
/Net/Snmp6/Icmp6OutNeighborSolicits
/Net/Snmp6/Icmp6OutParmProblems
/Net/Snmp6/Icmp6OutPktTooBigs
/Net/Snmp6/Icmp6OutRedirects
/Net/Snmp6/Icmp6OutRouterAdvertisements
/Net/Snmp6/Icmp6OutRouterSolicits
/Net/Snmp6/Icmp6OutTimeExcds
/Net/Snmp6/Icmp6OutType1
/Net/Snmp6/Icmp6OutType129
/Net/Snmp6/Icmp6OutType133
/Net/Snmp6/Icmp6OutType135
/Net/Snmp6/Icmp6OutType136
/Net/Snmp6/Icmp6OutType143
/Net/Snmp6/Ip6FragCreates
/Net/Snmp6/Ip6FragFails
/Net/Snmp6/Ip6FragOKs
/Net/Snmp6/Ip6InAddrErrors
/Net/Snmp6/Ip6InBcastOctets
/Net/Snmp6/Ip6InCEPkts
/Net/Snmp6/Ip6InDelivers
/Net/Snmp6/Ip6InDiscards
/Net/Snmp6/Ip6InECT0Pkts
/Net/Snmp6/Ip6InECT1Pkts
/Net/Snmp6/Ip6InHdrErrors
/Net/Snmp6/Ip6InMcastOctets
/Net/Snmp6/Ip6InMcastPkts
/Net/Snmp6/Ip6InNoECTPkts
/Net/Snmp6/Ip6InNoRoutes
/Net/Snmp6/Ip6InOctets
/Net/Snmp6/Ip6InReceives
/Net/Snmp6/Ip6InTooBigErrors
/Net/Snmp6/Ip6InTruncatedPkts
/Net/Snmp6/Ip6InUnknownProtos
/Net/Snmp6/Ip6OutBcastOctets
/Net/Snmp6/Ip6OutDiscards
/Net/Snmp6/Ip6OutForwDatagrams
/Net/Snmp6/Ip6OutMcastOctets
/Net/Snmp6/Ip6OutMcastPkts
/Net/Snmp6/Ip6OutNoRoutes
/Net/Snmp6/Ip6OutOctets
/Net/Snmp6/Ip6OutRequests
/Net/Snmp6/Ip6ReasmFails
/Net/Snmp6/Ip6ReasmOKs
/Net/Snmp6/Ip6ReasmReqds
/Net/Snmp6/Ip6ReasmTimeout
/Net/Snmp6/Udp6InCsumErrors
/Net/Snmp6/Udp6InDatagrams
/Net/Snmp6/Udp6InErrors
/Net/Snmp6/Udp6NoPorts
/Net/Snmp6/Udp6OutDatagrams
/Net/Snmp6/Udp6RcvbufErrors
/Net/Snmp6/Udp6SndbufErrors
/Net/Snmp6/UdpLite6InCsumErrors
/Net/Snmp6/UdpLite6InDatagrams
/Net/Snmp6/UdpLite6InErrors
/Net/Snmp6/UdpLite6NoPorts
/Net/Snmp6/UdpLite6OutDatagrams
/Net/Snmp6/UdpLite6RcvbufErrors
/Net/Snmp6/UdpLite6SndbufErrors
/Net/SocketsUsed

Имя метрики | Единица измерения | Метки | Описание
------------|-------------------|-------|---------
/Numa/Node/InterleaveHit | | `NumaNode` |
/Numa/Node/LocalNode | | `NumaNode` |
/Numa/Node/NumaForeign | | `NumaNode` |
/Numa/Node/NumaHit | | `NumaNode` |
/Numa/Node/NumaMiss | | `NumaNode` |
/Numa/Node/OtherNode | | `NumaNode` |

Имя метрики | Единица измерения | Метки | Описание
------------|-------------------|-------|---------
/Proc/La | | |
/Proc/LoadAverage1min | | |
/Proc/LoadAverage5min | | |
/Proc/LoadAverage15min | | |
/Proc/ProcsBlocked | | |
/Proc/ProcsRunning | | |
/Proc/ProcsSinceBoot | | |
/Proc/Threads | | |

Имя метрики | Единица измерения | Метки | Описание
------------|-------------------|-------|---------
/System/IdleTime | Микросекунды | `cpu` |
/System/IoWaitTime  | Микросекунды | `cpu` |
/System/IrqTime | Микросекунды | `cpu` |
/System/NiceTime | Микросекунды | `cpu` |
/System/SystemTime | Микросекунды | `cpu` |
/System/UpTime | | |
/System/UpTimeRaw | | |
/System/UserTime | Микросекунды | `cpu` |
