# 不定期重启



## 基本情况

硬件:

- gigabyte z390i wifi
- i9700k
- 970 evo 500GB for macos
- 970 evo 250GB for windows

现象是: 开启了睡眠之后, 唤醒的时候会偶然panic, 导致系统重启.

`pmset -g log` 观察到的日志为:

```bash
2021-04-11 16:03:05 +0800 Sleep                 Entering Sleep state due to 'Idle Sleep': Using AC (Charge:0%) 1803 secs
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleSystemSleep "com.apple.audio.context107.preventuseridlesleep" 10:13:58  id:0x0x100008105 [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleSystemSleep "com.apple.audio.context108.preventuseridlesleep" 10:13:58  id:0x0x100008108 [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleSystemSleep "com.apple.audio.context176.preventuseridlesleep" 01:54:15  id:0x0x10000829b [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleSystemSleep "com.apple.audio.context184.preventuseridlesleep" 01:54:15  id:0x0x1000082b7 [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleSystemSleep "com.apple.audio.context206.preventuseridlesleep" 01:53:44  id:0x0x1000083b0 [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleSystemSleep "com.apple.audio.context192.preventuseridlesleep" 01:54:15  id:0x0x1000082d5 [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleSystemSleep "com.apple.audio.context214.preventuseridlesleep" 01:53:44  id:0x0x1000083cc [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleSystemSleep "com.apple.audio.context148.preventuseridlesleep" 06:23:44  id:0x0x10000815b [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleDisplaySleep "com.apple.audio.context107.preventuseridledisplaysleep" 10:13:58  id:0x0x50000810b [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleDisplaySleep "com.apple.audio.context108.preventuseridledisplaysleep" 10:13:58  id:0x0x50000810e [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleDisplaySleep "com.apple.audio.context176.preventuseridledisplaysleep" 01:54:15  id:0x0x50000829c [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleDisplaySleep "com.apple.audio.context184.preventuseridledisplaysleep" 01:54:15  id:0x0x5000082b8 [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleDisplaySleep "com.apple.audio.context206.preventuseridledisplaysleep" 01:53:44  id:0x0x5000083b1 [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleDisplaySleep "com.apple.audio.context192.preventuseridledisplaysleep" 01:54:15  id:0x0x5000082d6 [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleDisplaySleep "com.apple.audio.context214.preventuseridledisplaysleep" 01:53:44  id:0x0x5000083cd [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleDisplaySleep "com.apple.audio.context148.preventuseridledisplaysleep" 06:23:44  id:0x0x50000815c [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleSystemSleep "com.apple.audio.context242.preventuseridlesleep" 00:56:53  id:0x0x10000877d [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleDisplaySleep "com.apple.audio.context242.preventuseridledisplaysleep" 00:56:53  id:0x0x50000877e [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleSystemSleep "com.apple.audio.context168.preventuseridlesleep" 01:54:17  id:0x0x10000824f [System: No Assertions]
2021-04-11 16:03:05 +0800 Assertions            PID 184(coreaudiod) Released PreventUserIdleDisplaySleep "com.apple.audio.context168.preventuseridledisplaysleep" 01:54:17  id:0x0x500008250 [System: No Assertions]
2021-04-11 16:03:06 +0800 Wake Requests         [process=dasd request=SleepService deltaSecs=90738 wakeAt=2021-04-12 17:15:24 info="com.apple.dasd:0:com.apple.apsd.apprefresh"] [*process=dasd request=TimerPlugin deltaSecs=1799 wakeAt=2021-04-11 16:33:05 info="com.apple.dasd:501:com.apple.Safari.SafeBrowsing.BrowsingDatabases.Update"] [process=mDNSResponder request=Maintenance deltaSecs=3529 wakeAt=2021-04-11 17:01:55 info="DHCP lease renewal"] [process=powerd request=UserWake deltaSecs=559831 wakeAt=2021-04-18 03:33:37 info="com.apple.alarm.user-visible-Weekly Usage Report,1424"]
2021-04-11 16:03:06 +0800 PM Client Acks        Delays to Sleep notifications: [com.apple.apsd is slow(1003 ms)]
2021-04-11 16:33:07 +0800 Assertions            PID 210(mDNSResponder) Created MaintenanceWake "mDNSResponder:maintenance" 00:00:00  id:0x0xd000089b1 [System: PrevIdle SRPrevSleep kCPU]
2021-04-11 16:33:07 +0800 AppWakeReason         AppWoke:com.apple.bluetoothd-blueavengers Reason:BlueAvengers: Toggle beacon state
2021-04-11 16:33:08 +0800 com.apple.sleepservices.sessionStarted        SleepService: window begins with cap time=86400 secs
2021-04-11 16:33:08 +0800 DarkWake              DarkWake from Normal Sleep [CDNPB] : due to RTC/Maintenance Using AC (Charge:0%) 75 secs
2021-04-11 16:33:08 +0800 HibernateStats        hibmode=0 standbydelaylow=86400 standbydelayhigh=86400                                    7
2021-04-11 16:33:08 +0800 WakeTime              WakeTime: 1.466 sec
2021-04-11 16:33:08 +0800 Kernel Client Acks    Delays to Sleep notifications: [AppleIntelFramebuffer driver is slow(msg: SetState to 1)(351 ms)] [vncserver timed out(30000 ms)] [laclient timed out(30000 ms)] [laclient timed out(30000 ms)] [AppleHDADriver driver is slow(msg: SetState to 0)(1020 ms)] [IOKernelDebugger driver is slow(msg: WillChangeState to 0)(5285 ms)]
2021-04-11 16:33:08 +0800 Kernel Client Acks    Delays to Wake notifications: [PRT0 driver is slow(msg: SetState to 2)(325 ms)] [IOKernelDebugger driver is slow(msg: DidChangeState to 1)(713 ms)] [PRT3 driver is slow(msg: SetState to 2)(1202 ms)] [PRT2 driver is slow(msg: SetState to 2)(1205 ms)] [PRT1 driver is slow(msg: SetState to 2)(1208 ms)]
2021-04-11 16:33:08 +0800 Assertions            PID 71(powerd) Summary BackgroundTask "Powerd - Wait for client BackgroundTask assertions" 00:00:00  id:0x0xb000089b9 [System: PrevIdle PushSrvc BGTask SRPrevSleep kCPU]
2021-04-11 16:33:08 +0800 Assertions            PID 101(apsd) Summary ApplePushServiceTask "com.apple.apsd-connectionestablish-push.apple.com" 00:00:01  id:0x0xb000089b5 [System: PrevIdle PushSrvc BGTask SRPrevSleep kCPU]
2021-04-11 16:33:08 +0800 Assertions            PID 71(powerd) Created InternalPreventSleep "com.apple.powermanagement.acwakelinger" 00:00:00  id:0x0xd000089bb [System: PrevIdle PushSrvc BGTask SRPrevSleep kCPU]
2021-04-11 16:33:08 +0800 Assertions            PID 210(mDNSResponder) Released MaintenanceWake "mDNSResponder:maintenance" 00:00:01  id:0x0xd000089b1 [System: PrevIdle PushSrvc BGTask SRPrevSleep kCPU]
2021-04-11 16:33:18 +0800 Assertions            PID 71(powerd) TimedOut ApplePushServiceTask "Powerd - Wait for client pushService assertions" 00:00:10  id:0x0xa000089ba [System: PrevIdle PushSrvc BGTask SRPrevSleep kCPU]
2021-04-11 16:33:18 +0800 Assertions            Summary- [System: PrevIdle PushSrvc BGTask SRPrevSleep kCPU] Using AC
2021-04-11 16:33:19 +0800 Assertions            PID 71(powerd) TimedOut BackgroundTask "Powerd - Wait for client BackgroundTask assertions" 00:00:10  id:0x0xb000089b9 [System: PrevIdle PushSrvc BGTask SRPrevSleep kCPU]
2021-04-11 16:33:22 +0800 Assertions            PID 101(apsd) Released InteractivePushServiceTask "com.apple.apsd-outgoingmessage" 00:00:11  id:0x0xa000089d7 [System: PrevIdle PushSrvc BGTask SRPrevSleep kCPU]
2021-04-11 16:33:27 +0800 Assertions            PID 101(apsd) Released InteractivePushServiceTask "com.apple.apsd-wakeconnection-push.apple.com" 00:00:19  id:0x0xa000089c0 [System: PrevIdle PushSrvc BGTask SRPrevSleep kCPU]
2021-04-11 16:33:34 +0800 Assertions            PID 101(apsd) Released InteractivePushServiceTask "com.apple.apsd-outgoingmessage" 00:00:10  id:0x0xa000089e3 [System: PrevIdle PushSrvc BGTask SRPrevSleep kCPU]
2021-04-11 16:33:46 +0800 Assertions            PID 101(apsd) Released InteractivePushServiceTask "com.apple.apsd-outgoingmessage" 00:00:10  id:0x0xa000089ea [System: PrevIdle PushSrvc BGTask SRPrevSleep kCPU]
2021-04-11 16:33:47 +0800 com.apple.sleepservices.sessionTerminated     SleepService: window has terminated.
2021-04-11 16:33:48 +0800 Assertions            PID 1436(identityservicesd) Released PreventUserIdleSystemSleep "IDSPeerIDLookup" 00:00:36  id:0x0x1000089d5 [System: BGTask SRPrevSleep kCPU]
2021-04-11 16:33:53 +0800 Assertions            PID 71(powerd) TimedOut InternalPreventSleep "com.apple.powermanagement.acwakelinger" 00:00:45  id:0x0xd000089bb [System: BGTask SRPrevSleep kCPU]
2021-04-11 16:34:22 +0800 Assertions            PID 1424(UserEventAgent) Released BackgroundTask "com.apple.mediaanalysisd.fullanalysis" 00:01:13  id:0x0xb000089c8 [System: BGTask kCPU]
2021-04-11 16:34:23 +0800 Sleep                 Entering Sleep state due to 'Maintenance Sleep': Using AC (Charge:0%) 849 secs
2021-04-11 16:34:24 +0800 Wake Requests         [process=dasd request=SleepService deltaSecs=88958 wakeAt=2021-04-12 17:17:03 info="com.apple.dasd:0:com.apple.apsd.apprefresh"] [*process=dasd request=TimerPlugin deltaSecs=2080 wakeAt=2021-04-11 17:09:04 info="com.apple.dasd:0:com.apple.backupd-auto"] [process=mDNSResponder request=Maintenance deltaSecs=6414 wakeAt=2021-04-11 18:21:19 info="DHCP lease renewal"] [process=powerd request=UserWake deltaSecs=557952 wakeAt=2021-04-18 03:33:37 info="com.apple.alarm.user-visible-Weekly Usage Report,1424"]
2021-04-11 16:34:24 +0800 PM Client Acks        Delays to Sleep notifications: [com.apple.apsd is slow(1772 ms)]
2021-04-11 16:48:31 +0800 Assertions            PID 210(mDNSResponder) Created MaintenanceWake "mDNSResponder:maintenance" 00:00:00  id:0x0xd00008a00 [System: SRPrevSleep kCPU]
2021-04-11 16:48:31 +0800 Assertions            PID 210(mDNSResponder) Released MaintenanceWake "mDNSResponder:maintenance" 00:00:00  id:0x0xd00008a00 [System: PrevIdle]
2021-04-11 16:48:32 +0800 Assertions            PID 71(powerd) Created InternalPreventSleep "PM configd - Wait for Device enumeration" 00:00:00  id:0x0xd00008a0a [System: SRPrevSleep kCPU]
2021-04-11 16:48:32 +0800 com.apple.sleepservices.sessionStarted        SleepService: window begins with cap time=86400 secs
2021-04-11 16:48:32 +0800 DarkWake              DarkWake from Normal Sleep [CDNP] : due to XDCI CNVW/ Using AC (Charge:0%) 45 secs
2021-04-11 16:48:32 +0800 HibernateStats        hibmode=0 standbydelaylow=86400 standbydelayhigh=86400                                    8
2021-04-11 16:48:32 +0800 WakeTime              WakeTime: 1.454 sec
2021-04-11 16:48:32 +0800 Kernel Client Acks    Delays to Sleep notifications: [AppleIntelFramebuffer driver is slow(msg: SetState to 1)(351 ms)] [vncserver timed out(30000 ms)] [laclient timed out(30000 ms)] [laclient timed out(30000 ms)] [AppleHDADriver driver is slow(msg: SetState to 0)(1020 ms)] [IOKernelDebugger driver is slow(msg: WillChangeState to 0)(5285 ms)]
2021-04-11 16:48:32 +0800 Kernel Client Acks    Delays to Wake notifications: [PRT0 driver is slow(msg: SetState to 2)(325 ms)] [IOKernelDebugger driver is slow(msg: DidChangeState to 1)(713 ms)] [PRT3 driver is slow(msg: SetState to 2)(1202 ms)] [PRT2 driver is slow(msg: SetState to 2)(1205 ms)] [PRT1 driver is slow(msg: SetState to 2)(1208 ms)] [IOKernelDebugger driver is slow(msg: WillChangeState to 0)(5292 ms)] [PRT0 driver is slow(msg: SetState to 2)(647 ms)] [IOKernelDebugger driver is slow(msg: DidChangeState to 1)(699 ms)] [PRT3 driver is slow(msg: SetState to 2)(1207 ms)] [PRT1 driver is slow(msg: SetState to 2)(1208 ms)] [PRT2 driver is slow(msg: SetState to 2)(1208 ms)]
2021-04-11 16:48:32 +0800 Assertions            PID 71(powerd) Created InternalPreventSleep "com.apple.powermanagement.acwakelinger" 00:00:00  id:0x0xd00008a0c [System: PushSrvc SRPrevSleep kCPU]
2021-04-11 16:48:42 +0800 Assertions            PID 71(powerd) TimedOut ApplePushServiceTask "Powerd - Wait for client pushService assertions" 00:00:10  id:0x0xa00008a0b [System: PushSrvc SRPrevSleep kCPU]
2021-04-11 16:48:44 +0800 com.apple.sleepservices.sessionTerminated     SleepService: window has terminated.
2021-04-11 16:49:17 +0800 Assertions            PID 71(powerd) Released InternalPreventSleep "PM configd - Wait for Device enumeration" 00:00:45  id:0x0xd00008a0a [System: SRPrevSleep kCPU]
2021-04-11 16:49:17 +0800 Assertions            PID 71(powerd) TimedOut InternalPreventSleep "com.apple.powermanagement.acwakelinger" 00:00:45  id:0x0xd00008a0c [System: SRPrevSleep kCPU]
2021-04-11 16:49:17 +0800 Assertions            Summary- [System: No Assertions] Using AC
2021-04-11 16:49:17 +0800 Sleep                 Entering Sleep state due to 'Maintenance Sleep': Using AC (Charge:0%)
2021-04-11 16:49:18 +0800 Wake Requests         [process=dasd request=SleepService deltaSecs=87960 wakeAt=2021-04-12 17:15:18 info="com.apple.dasd:0:com.apple.apsd.apprefresh"] [*process=dasd request=TimerPlugin deltaSecs=1196 wakeAt=2021-04-11 17:09:14 info="com.apple.dasd:0:com.apple.backupd-auto"] [process=mDNSResponder request=Maintenance deltaSecs=5610 wakeAt=2021-04-11 18:22:48 info="DHCP lease renewal"] [process=powerd request=UserWake deltaSecs=557059 wakeAt=2021-04-18 03:33:37 info="com.apple.alarm.user-visible-Weekly Usage Report,1424"]
2021-04-11 16:49:18 +0800 PM Client Acks        Delays to Sleep notifications: [com.apple.apsd is slow(1002 ms)]
2021-04-11 16:50:48 +0800 ShutdownCause         SMC shutdown cause: 5: Software initiated shutdown
2021-04-11 16:50:49 +0800 HibernateStats        hibmode=0 standbydelaylow=0 standbydelayhigh=0                                            0

```

可以看到若干的sleep/wake流程, 最后是 `SMC shutdown cause: 5: Software initiated shutdown`

`cause 5` 查到的原因是正常关机([link](https://apple.stackexchange.com/questions/126588/are-os-x-shutdown-cause-and-sleep-cause-numbers-listed-explained-anywhere)), 但其实一点都不正常.

重启进入桌面后, 在"是否反馈给Apple"的对话框中, 查看到的panic信息如下:

```bash
panic(cpu 0 caller 0xffffff8018386d06): nvme: "Fatal error occurred. CSTS=0x1 US[1]=0x0 US[0]=0x0 VID=0x144d DID=0xa808
. FW Revision=\n"@/AppleInternal/BuildRoot/Library/Caches/com.apple.xbs/Sources/IONVMeFamily/IONVMeFamily-557.60.1/Common/IONVMeController.cpp:5472
Backtrace (CPU 0), Frame : Return Address
0xffffffa0f1a8b960 : 0xffffff8015cbab4d mach_kernel : _handle_debugger_trap + 0x3dd
0xffffffa0f1a8b9b0 : 0xffffff8015dfd7e3 mach_kernel : _kdp_i386_trap + 0x143
0xffffffa0f1a8b9f0 : 0xffffff8015dede1a mach_kernel : _kernel_trap + 0x55a
0xffffffa0f1a8ba40 : 0xffffff8015c5fa2f mach_kernel : _return_from_trap + 0xff
0xffffffa0f1a8ba60 : 0xffffff8015cba3ed mach_kernel : _DebuggerTrapWithState + 0xad
0xffffffa0f1a8bb80 : 0xffffff8015cba6d8 mach_kernel : _panic_trap_to_debugger + 0x268
0xffffffa0f1a8bbf0 : 0xffffff80164bef9a mach_kernel : _panic + 0x54
0xffffffa0f1a8bc60 : 0xffffff8018386d06 com.apple.iokit.IONVMeFamily : __ZN16IONVMeController14CommandTimeoutEP16AppleNVMeRequest.cold.1
0xffffffa0f1a8bc80 : 0xffffff801836b427 com.apple.iokit.IONVMeFamily : __ZN16IONVMeController13FatalHandlingEv + 0x1af
0xffffffa0f1a8bde0 : 0xffffff801641d385 mach_kernel : __ZN18IOTimerEventSource15timeoutSignaledEPvS0_ + 0xa5
0xffffffa0f1a8be50 : 0xffffff801641d286 mach_kernel : __ZN18IOTimerEventSource17timeoutAndReleaseEPvS0_ + 0xc6
0xffffffa0f1a8be80 : 0xffffff8015cff725 mach_kernel : _thread_call_delayed_timer + 0x4a5
0xffffffa0f1a8bef0 : 0xffffff8015d00634 mach_kernel : _thread_call_delayed_timer + 0x13b4
0xffffffa0f1a8bfa0 : 0xffffff8015c5f13e mach_kernel : _call_continuation + 0x2e
      Kernel Extensions in backtrace:
         com.apple.iokit.IONVMeFamily(2.1)[D5DFC80E-EF7A-3660-BE57-473E67626B44]@0xffffff8018364000->0xffffff801838dfff
            dependency: com.apple.driver.AppleEFINVRAM(2.1)[D6C13E44-3657-3F40-99E4-355DAA82202E]@0xffffff801705a000->0xffffff8017063fff
            dependency: com.apple.driver.AppleMobileFileIntegrity(1.0.5)[2A454117-CDAA-301F-B609-BA396742C91A]@0xffffff8017201000->0xffffff8017215fff
            dependency: com.apple.iokit.IOPCIFamily(2.9)[BF2C5E86-1E8F-3FD4-9874-7738178FA73B]@0xffffff801861f000->0xffffff8018646fff
            dependency: com.apple.iokit.IOReportFamily(47)[D3C4FAA4-8F06-3C5C-AB36-4BE632CCE051]@0xffffff8018655000->0xffffff8018657fff
            dependency: com.apple.iokit.IOStorageFamily(2.1)[B5300908-BF34-3D47-8776-FB154A6DEE4C]@0xffffff801873f000->0xffffff8018750fff

Process name corresponding to current thread: kernel_task
Boot args: -v debug=0x100 keepsyms=1 igfxonln=1 chunklist-security-epoch=0 -chunklist-no-rev2-dev

Mac OS version:
20D91

Kernel version:
Darwin Kernel Version 20.3.0: Thu Jan 21 00:07:06 PST 2021; root:xnu-7195.81.3~1/RELEASE_X86_64
Kernel UUID: C86236B2-4976-3542-80CA-74A6B8B4BA03
KernelCache slide: 0x0000000015a00000
KernelCache base:  0xffffff8015c00000
Kernel slide:      0x0000000015a10000
Kernel text base:  0xffffff8015c10000
__HIB  text base: 0xffffff8015b00000
System model name: iMac19,1 (Mac-AA95B1DDAB278B95)
System shutdown begun: NO
Panic diags file available: YES (0x0)
Hibernation exit count: 0

System uptime in nanoseconds: 8207276766376
Last Sleep:           absolute           base_tsc          base_nano
  Uptime  : 0x00000776e7d0fb2a
  Sleep   : 0x00000764d3191765 0x00000017920caa32 0x0000000000000000
  Wake    : 0x00000765342c307f 0x00000000d66a599c 0x000007651cda9907
```

猜测到应该是 macOS 唤醒 nvme 硬盘的时候出现了问题



## 尝试: 禁用不必要的唤醒

根据 opencore fix sleep 的[文档](https://dortania.github.io/OpenCore-Post-Install/universal/sleep.html#preparations) 做了很多尝试:

- 禁用不必要的唤醒

  ```bash
  # macOS 终端内执行
  sudo pmset autopoweroff 0
  sudo pmset powernap 0
  sudo pmset standby 0
  sudo pmset proximitywake 0
  sudo pmset tcpkeepalive 0
  
  # opencore config 修改
  Misc -> Boot -> HibernateMode -> None
  
  # BIOS 修改
  Wake on LAN -> Disable
  Trusted Platform Module -> Disable
  ```

  

用了一段时间看看日志, 还是看到了一些系统的自动唤醒, 看日志是`alarm.user-visible-Weekly Usage Report`, 然后 System Report -> Power 里也有电源的自动唤醒任务. 应该是 Screen Time 的功能导致的, 去系统设置里关掉它, 关掉所有已有的计划任务:

```bash
pmset schedule cancelall
```

再用一段时间, 查看 `pmset -g log` , 只有系统空闲后的自动休眠, 以及通过键盘的手动唤醒:

```bash
2021-04-18 03:27:59 +0800 Sleep                 Entering Sleep state due to 'Idle Sleep': Using AC (Charge:0%) 23495 secs
2021-04-18 03:28:01 +0800 PM Client Acks        Delays to Sleep notifications: [com.apple.apsd is slow(1993 ms)]
2021-04-18 09:59:34 +0800 DarkWake              DarkWake from Normal Sleep [CDN] : due to XDCI CNVW/ Using AC (Charge:0%) 4 secs
2021-04-18 09:59:34 +0800 Kernel Client Acks    Delays to Sleep notifications: [vncserver timed out(30000 ms)] [laclient timed out(30000 ms)] [vncserver timed out(30000 ms)] [laclient timed out(30000 ms)] [AppleHDADriver driver is slow(msg: SetState to 0)(1020 ms)] [IOKernelDebugger driver is slow(msg: WillChangeState to 0)(5290 ms)]
2021-04-18 09:59:34 +0800 Kernel Client Acks    Delays to Wake notifications: [PRT0 driver is slow(msg: SetState to 2)(666 ms)] [IOKernelDebugger driver is slow(msg: DidChangeState to 1)(697 ms)] [PRT3 driver is slow(msg: SetState to 2)(1143 ms)] [PRT2 driver is slow(msg: SetState to 2)(1145 ms)] [PRT1 driver is slow(msg: SetState to 2)(1148 ms)]
2021-04-18 09:59:38 +0800 Wake                  DarkWake to FullWake from Normal Sleep [CDNVA] : due to UserActivity Assertion Using AC (Charge:0%)
2021-04-18 09:59:38 +0800 Kernel Client Acks    Delays to Sleep notifications: [vncserver timed out(30000 ms)] [laclient timed out(30000 ms)] [vncserver timed out(30000 ms)] [laclient timed out(30000 ms)] [AppleHDADriver driver is slow(msg: SetState to 0)(1020 ms)] [IOKernelDebugger driver is slow(msg: WillChangeState to 0)(5290 ms)]
2021-04-18 09:59:38 +0800 Kernel Client Acks    Delays to Wake notifications: [PRT0 driver is slow(msg: SetState to 2)(666 ms)] [IOKernelDebugger driver is slow(msg: DidChangeState to 1)(697 ms)] [PRT3 driver is slow(msg: SetState to 2)(1143 ms)] [PRT2 driver is slow(msg: SetState to 2)(1145 ms)] [PRT1 driver is slow(msg: SetState to 2)(1148 ms)] [AppleHDAHDMI_DPDriver driver is slow(msg: SetState to 1)(456 ms)] [AppleIntelFramebuffer driver is slow(msg: SetState to 2)(467 ms)] [AppleIntelFramebuffer driver is slow(msg: DidChangeState to 2)(467 ms)] [AppleIntelFramebuffer driver is slow(msg: DidChangeState to 2)(357 ms)] [AppleHDADriver driver is slow(msg: SetState to 1)(1615 ms)]

```

但是还是有遇到唤醒就panic 然后系统重启的情况, 崩溃日志还是指向了 nvme.



## 尝试: nvmefix.kext

加入 [nvmefix.kext](https://github.com/acidanthera/NVMeFix), 问题依旧

## 尝试: 禁用另一块nvme硬盘

后来在 reddit 看到一个哥们说他 [双nvme硬盘遇到了问题](https://www.reddit.com/r/hackintosh/comments/lc0xgp/nvmefixkext_creates_kernel_panic_when_theres_more/), 决定把装windows 的另一块 nvme 硬盘禁用掉试试, 按[禁用显卡](https://dortania.github.io/Getting-Started-With-ACPI/Desktops/desktop-disable.html)的文档:

- 找到硬盘控制器的 acpi 路径. 注意是 storage controllers , 而不是 disk drives.

- 编辑示例的 SSDT-GPU-DISABLE.dsl, 替换到对应的 acpi 路径

- 用 maciASL 把 dsl 文件编译为 aml 文件, 我改了名字: SSDT-NVME-DISABLE.aml,  放到 EFI/OC/ACPI 文件夹内

- 编辑 EFI/OC/config.plist, 在 ACPI -> ADD 里加了一段:

  ```bash
  			<dict>
  				<key>Comment</key>
  				<string>disable windows nvme drive</string>
  				<key>Enabled</key>
  				<true/>
  				<key>Path</key>
  				<string>SSDT-NVME-DISABLE.aml</string>
  			</dict>
  ```

  

# todo

如果还无效, 那么可以试试:

- `forceRenderStandby=0` [1193](https://github.com/acidanthera/bugtracker/issues/1193)