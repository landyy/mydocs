---
category: Native API
title: 'NtQueryInformationThread'

layout: nil
---

### NtQueryInformationThread

NtQueryInformationThread function can be defined as below:

```
typedef NTSTATUS(WINAPI *NtQueryThreadPointer)(
IN HANDLE          ThreadHandle,
IN THREADINFOCLASS ThreadInformationClass,
OUT PVOID          ThreadInformation,
IN ULONG           ThreadInformationLength,
OUT PULONG         ReturnLength);
```

With the pointer defined, we can use GetProcAddress to actually locate the function and get a pointer to it

```
NtQueryThreadPointer NtQueryInformationThread = (NtQueryThreadPointer)GetProcAddress(
	GetModuleHandle(L"ntdll.dll"), 
	"NtQueryInformationThread");
```

The variable, "NtQueryInformationThread" can now be used to call the function itself.

While most of the vars passed are straight forward, the THREADINFOCLASS is of biggest interest and will change the most. Below is a list with a small description of different variations of the THREADINFOCLASS.

```
0x00	ThreadBasicInformation
0x01 	ThreadTimes
0x02 	ThreadPriority 
0x03 	ThreadBasePriority 
0x04 	ThreadAffinityMask
0x05 	ThreadImpersonationToken
0x06 	ThreadDescriptorTableEntry 
0x07 	ThreadEnableAlignmentFaultFixup 
0x08 	ThreadEventPair 
0x09 	ThreadQuerySetWin32StartAddress
0x0A 	ThreadZeroTlsCell
0x0B 	ThreadPerformanceCount 
0x0C 	ThreadAmILastThread 
0x0D 	ThreadIdealProcessor 
0x0E 	ThreadPriorityBoost 
0x0F 	ThreadSetTlsArrayAddress 
0x10 	ThreadIsIoPending
0x11 	ThreadHideFromDebugger
0x12 	ThreadBreakOnTermination
0x13 	ThreadSwitchLegacyState
0x14 	ThreadIsTerminated 
0x15 	ThreadLastSystemCall
0x16 	ThreadIoPriority 
0x17 	ThreadCycleTime 
0x18 	ThreadPagePriority
0x19 	ThreadActualBasePriority 
0x1A 	ThreadTebInformation
0x1B 	ThreadCSwitchMon 
0x1C 	ThreadCSwitchPmu 
0x1D 	ThreadWow64Context 
0x1E 	ThreadGroupInformation 
0x1F 	ThreadUmsInformation 
0x20 	ThreadCounterProfiling
0x21 	ThreadIdealProcessorEx
0x22 	ThreadCpuAccountingInformation
0x23 	ThreadSuspendCount
0x24 	ThreadHeterogeneousCpuPolicy 
0x25 	ThreadContainerId 
0x26 	ThreadNameInformation 
0x27 	ThreadSelectedCpuSets 
0x28 	ThreadSystemThreadInformation 
0x29 	ThreadActualGroupAffinity
```

NtQueryInformationThread provides much more detail on threads that are running. For whatever reasons, the regular API does not do this so we are stuck with using this.