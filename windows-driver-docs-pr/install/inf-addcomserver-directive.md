---
title: INF AddComServer directive
description: An AddComServer directive is used within a DDInstall.COM section and registers a COM server.
ms.date: 04/17/2024
ms.topic: reference
---

# INF AddComServer directive

An AddComServer directive is used within a DDInstall.COM section and registers a COM server. One or more COM servers must be defined in a DDInstall.COM section. This section is supported for Windows 11 version 24H2 and later.

```inf
[DDInstall.COM]

AddComServer = com-server-name, [flags], com-server-install-section
```

## Entries

### com-server-name

Specifies the name of the COM server being installed. The name is generally the name or description of the COM component being registered. The COM server name must be unique within the INF and is used as the description when the COM class description is missing.

### flags

Specifies extra flags for the AddComServer directive. The flags field is reserved for future use and should be left blank or set to zero.

### com-server-install-section

References an INF-writer-defined section that contains information for registering the COM server and its classes.

For more information on the COM server install section, see the following Remarks, and for COM servers in general, see [COM Clients and Servers](/windows/win32/com/com-clients-and-servers).

## Remarks

The *AddComServer* directive causes system setup to register a COM server implemented by a server binary in a driver package's [driver store relative path](../develop/run-from-driver-store.md).

**[CoRegisterDeviceCatalog](/windows/win32/api/combaseapi/nf-combaseapi-coregisterdevicecatalog)** must be called in every process before calling **[CoCreateInstance](/windows/win32/api/combaseapi/nf-combaseapi-cocreateinstance)** on the COM class. Calling **CoRegisterDeviceCatalog** makes the COM server registrations available in the process for the COM runtime to use.

Each *AddComServer* directive in an INF DDInstall.COM section can reference an INF-writer-defined com-server-install-section elsewhere in the INF file. Each INF-writer-defined section name must be unique within the INF file and must follow the general rules for defining section names. For more information about these rules, see [General Syntax Rules for INF Files](general-syntax-rules-for-inf-files.md).

An *AddComServer* directive must reference a named com-server-install-section elsewhere in the INF. Each such section has the following form:

```inf
[com-server-install-section]

ServerType            = server-type
ServerBinary          = binary-path
[ServerBinaryWow64    = wow64-binary-path]
AddComClass           = {clsid-guid}[, flags[, com-class-install-section]]
```

Each *com-server-install-section* must provide **ServerType**, **ServerBinary** and one or more **AddComClass**, each on a separate line.

## com-server-install-section entries and values

**ServerType**

Specifies type of COM server that is being registered. Each COM server type has a specific set of required and optional entries and directives. *Only 0x1 (In-proc) is supported.*

| server-type-enum | Server type | Required directives | Optional directives |
|---|---|---|---|
| 0x1 | In-proc | <ul><li>ServerBinary</li><li>AddComClass</li></ul> | <ul><li>ServerBinaryWow64</li><li>ThreadingModel</li></ul> |

**ServerBinary**

Path to COM server binary for native architecture.

**ServerBinaryWow64**

Path to COM server WOW64 binary for non-native x86 architecture support on AMD64 platform.

**AddComClass** = {clsid-guid}[, flags[, com-class-install-section]]

This required directive can be used one or more times to register COM classes with optional install sections.

For more information on how to register COM classes, see [INF AddComClass Directive](inf-addcomclass-directive.md).

## Example

```inf
[ContosoEncoderServer.NT.COM]
AddComServer   = ContosoEncoderServer,, ContosoEncoder_ComServer_Inst

[ContosoEncoder_ComServer_Inst]
ServerType     = 1 ; in-proc
ServerBinary   = %13%\contoso_encoder.dll
AddComClass    = {bb2b85ab-9473-42e5-8d1a-0f01d3879879}
AddComClass    = {f1baf99b-d28a-4ea3-b652-355da082d260}, 0, ContosoEncoderControl_ComClass_Inst

[ContosoEncoderControl_ComClass_Inst]
Description    = %ContosoEncoder_Comclass_Desc%
ThreadingModel = Apartment

[Strings]
%ContosoEncoder_Comclass_Desc%="Contoso H.264 Encoder"
```

## See also

- [Using a Component INF File](using-a-component-inf-file.md)
- [INF DDInstall.COM section](inf-ddinstall-com-section.md)
- [INF AddComClass directive](inf-addcomclass-directive.md)
- [INF AddInterface directive](inf-addinterface-directive.md)
