---
category: Native API
title: 'WinStationSendMessageW'

layout: nil
---

### WinStationSendMessageW

WinStationSendMessageW is an undocumented function that allows you to send messages to other users on the system in the form of a text box. It can be defined as below:

```WinStationSendMessageW(
	IN HANDLE hServer,
	IN ULONG SessionId
	IN LPCWSTR Title,
	IN ULONG TitleLength,
	IN LPCWSTR Message,
	IN ULONG MessageLength,
	IN ULONG Style,
	IN ULONG Timeout,
	OUT PULONG Response,
	IN BOOLEAN DoNotWait
 );```

Since it is undocumented and not parted of the loaded moduled, we must use the LoadLibrary Function to get a handle to the module

```auto hModule = LoadLibrary(L"C:\\Windows\\System32\\winsta.dll");
 
WinStationSendMessageWPtr WinStationSendMessageW = (WinStationSendMessageWPtr)GetProcAddress(hModule ,"WinStationSendMessageW");```

An example of a message being sent to a user with a interactive console session (Session ID: 1) below:

```WinStationSendMessageW(
    NULL,
    1,
    testtitle,
    wcslen(testtitle) * 4 + 1, //yeah idk how you get the proper length of an LPCWSTR
    testtext,
    wcslen(testtext) * 4 + 1,  //its a guess tbh
    MB_YESNO| MB_ICONWARNING,
    0,
    &response,
    TRUE
);```