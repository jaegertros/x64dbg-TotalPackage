
== Files
- OllyDumpEx_Od11.dll
  for OllyDbg version 1.10 (1.10 tested)
- OllyDumpEx_Od20.dll
  for OllyDbg version 2.01 (2.01 tested)
- OllyDumpEx_Imm18.dll
  for Immunity Debugger version 1.8x or higher (1.85 tested)
- OllyDumpEx_IdaRT.plw, OllyDumpEx_IdaRT.p64
  for IDA Pro 32bit build version 5.x or higher (6.9 tested)
- OllyDumpEx_IdaRT.dll, OllyDumpEx_IdaRT64.dll
  for IDA Pro 64bit build version 7.0 or higher (7.1 tested)
- OllyDumpEx_IdaFW.plw
  for IDA Freeware 32bit build version 5.0 (5.0 tested)
- OllyDumpEx_IdaFW64.dll
  for IDA Freeware 64bit build version 7.0 (7.0.190307 tested)
- OllyDumpEx_Wd32.dll, OllyDumpEx_Wd64.dll
  for WinDbg version 6.x (6.2 tested)
- OllyDumpEx_X64Dbg.dp32, OllyDumpEx_X64Dbg.dp64
  for x64dbg (snapshot 20170822 tested)
- OllyDumpEx_SA32.exe, OllyDumpEx_SA64.exe
  Standalone version


== Known Issue
- Incorrect memory attribute
  OllyDbg 1.10 and Immunity Debugger Image type memory is always readonly.
  IDA Pro cannot detect Mapped type, Guard, CopyOnWrite attribute.
- All Memory Search mode hit listed module
  OllyDbg 1.10 and Immunity Debugger not refresh t_memory table automatically.
  Open Memory window and refresh (ALT+M) before search.
- Cannot search memory address greater than 0x7FFFFFFF
  OllyDbg 2.01h seems to be 0x80000000-0xFFFEFFFF memory range as kernel memory 
  even if debuggee compiled with LARGEADDRESSAWARE option.
- 64bit Limitation
  ImageBase change not supported.
- ELF Limitation
  Rebuild mode only available on IDA Pro due to other debuggers not support ELF.
- BinaryDump mode behavior
  Memory: No modification.
  File  : Overwrite by header data from file.
  Dummy : Overwrite by dummy header and add whole data as one section.
- Dumped ELF binary not work (FAQ)
  Try disable lazy binding using env LD_BIND_NOW=1, just ignore PLTGOT inconsistency.
- Dumped UPX binary not work (FAQ)
  Disable "Prefer Original Characteristics" option before dump.
  Problem is PE characteristics and memory access permission inconsistency.


== Changelog
- v1.80 / 2020-01-06
  Bugfix: Fix race condition when reading large amount of memory (IDA)
  Bugfix: DYNAMICBASE not working (Standalone)
  Bugfix: Fix UI stall race condition issue when press Back to Menu button
  Improve: Adjust UI layout for high DPI setting
  Improve: Add DebugPriv button for runas administrator (Standalone)
  Improve: Add OpenFile button for carving from localfile (Standalone)
  Improve: Resolve mapped filename if possible (Standalone,x64dbg)
  Improve: Add ReScan marker for rescan required setting changes
  Improve: Use segment name as module name when segment not belong to module (IDA)
  Improve: Address range autofill use mapped address instead of image base address
  Add: File image source use specified file when memory and address base mode selected
  Add: Dummy image header mode for image which not have valid image header
- v1.72 / 2019-03-14
  Improve: Support IDA Freeware with debugger version 7.0.190307
- v1.70 / 2018-08-14
  Bugfix: Dump feature not working when non-executable file loaded (IDA)
  Bugfix: Readmemory sign extended issue (WinDbg)
  Bugfix: Fix Virtual Offset not working on PE32
  Bugfix: Fix duplicated entry in section list
  Improve: Get EIP as OEP button disabled when debugger not active
  Improve: Add EFI and windows driver type detection 
  Improve: Better fix for corrupted PE IMAGE_DIRECTORY_ENTRY
  Improve: Add Cancel feature to search and dump
  Add: Search All Occurrences option and Search Result list
- v1.64 / 2018-05-10
  Improve: Follow IDA 7.1 changes which break callui backward compatibility layer
  Improve: Dump feature available even if debuggee not running (IDA)
  Add: Support IDA Freeware version 7.0 (EXPERIMENTAL)
- v1.62 / 2017-11-05
  Bugfix: Rebuild dumpfile corrupted when ELF PT_PHDR entry not exist
  Bugfix: Failed to load ELF header when sparse segment layout
  Improve: Corrupted ELF structure handling
  Improve: ELF Loader segment always aligned same as mmap behavior
- v1.60 / 2017-09-19
  Add: ELF support
  Add: Standalone version
  Add: Support IDA Pro 64bit build plugin interface (7.0)
  Improve: Image Size editable in binary dump mode for overlay data
  Del: Drop old version of Immunity Debugger support (1.7x)
- v1.50 / 2015-07-03
  Add: Fuzzy Search mode (for corrupted MZ/PE Signature) 
  Add: Fix Corrupted PE Header option (Fill Hole option is merged)
  Add: Dump result dialog for copy and paste
  Improve: Search method optimization
  Improve: Corrupted PE Header handling
  Improve: Binary dump mode support some options
  Bugfix: Rebased PE handling (rebuild dump mode)
  Bugfix: Debuggee filename error on attached process (IDA)
  Bugfix: Get EIP does not work in recent version (x64_dbg)
- v1.40 / 2014-12-17
  Add: Support x64_dbg plugin interface (both 32bit and 64bit)
  Improve: Enable NXCOMPAT and DYNAMICBASE for plugin binaries
- v1.30 / 2013-06-28
  Add: Support WinDbg plugin interface (both 32bit and 64bit)
  Improve: Add plugin name and version directory to archive file 
  Bugfix: Data after section headers in PE Header has been ignored
  Bugfix: Fix SizeOfHeaders inconsistency
- v1.20 / 2013-05-27
  Add: Support IDA Pro plugin interface (both Retail and Freeware version)
  Add: Support native 64bit process dump (IDA Pro only)
  Improve: Change dialog position to center of parent window
  Improve: Add debug toggle menu to dialog system menu
  Improve: Section size handling single section belongs to multiple memory segments
  Bugfix: Zero virtual size section handling
- v1.12 / 2013-04-02
  Improve: Update to OllyDbg 2 latest version PDK (2.01h, PLUGIN_VERSION 0x02010001)
  Improve: Tested with latest version of debuggers (OllyDbg 2.01h and Immunity Debugger 1.85)
  Bugfix: Search greater than 0x7FFFFFFF memory address failed (IMAGE_FILE_LARGE_ADDRESS_AWARE)
- v1.10 / 2013-03-24
  Add: Search type All Memory
  Add: Binary dump mode (no rebuild PE header, for before load image)
  Add: PE32+ support (Binary dump mode only)
  Add: Memory Address/Size parameters editable (dump source address)
  Improve: Add info message for Relocation Flag and EXE/DLL type
  Improve: Large PE Header handling (larger than 0x1000)
  Improve: Check SectionAlignment and FileAlignment consistency
  Improve: Reduce search memory usage (not depend on target memory size)
  Improve: Detect PE Header across different type pages (parse and search)
  Bugfix: Improper owner window handle 
  Bugfix: Section not listed when belong memory range not exists
  Bugfix: Almost features broken when memory window sort order changed
- v1.00 / 2013-03-12
  Add: Selectable Base PE Header (Module/Memory/Address)
  Add: Search PE Header from memory
  Improve: PE Source default change Disk to Memory
  Improve: ASLR aware (except PE Source from Disk mode)
  Improve: Clear DynamicBase DllCharacteristics flag with Disable Relocation option
  Improve: PE Header parse and modify more carefully (corrupt PE handling)
  Improve: Inherit selected address from memory window
  Bugfix: Fix Virtual Offset feature cause crash (divide by zero)
  Bugfix: Parse invalid sections cause crash
- v0.92 / 2012-10-09
  Improve: Support OllyDbg version 2 plugin new interface
- v0.90 / 2011-08-24
  Add: Support OllyDbg version 2 plugin interface (EXPERIMENTAL)
  Improve: Rewrite Wide/Multibyte-Character support code
  Improve: Decode CopyOnWrite page attribute
  Bugfix: Detect working directory (Wide-Character only)
- v0.80 / 2011-08-01
  Add: Support Immunity Debugger version 1.8x or higher
  Improve: Data Directory rebuild option (check rewrite range)
  Improve: Always round up PE header size to 0x1000 (ImportRec not extend itself)
  Bugfix: TLS Data Directory ignored
- v0.70 / 2011-07-07
  Add: Support Immunity Debugger version 1.7x or lower
  Improve: Data Directory rebuild option (support ImportTable)
  Improve: Image Base Address alignment checking
  Improve: Virtual Offset Address alignment checking
- v0.60
  Improve: DeSelect is too slow when Auto Adjust Image Base option enabled
  Add: Virtual Offset Address overlap checking
- v0.50
  Improve: Data Directory rebuild option (support ResourceDirectory)
  Add: Auto Adjust Image Base Address option
- v0.40
  Add: Data Directory rebuild option for RVA Adjust (support ExportTable)
  Improve: Invalid Image Base checking
  Improve: Virtual Offset overlap checking
- v0.30
  Add: Section sort by Virtual Offset
  Add: Fill Virtual Offset Hole option
- v0.20
  Bugfix: Fix many bugs 
- v0.10
  Initial version


== Bug Report
  Please try latest version before report. 
  With your environment detail, logs and way to reproduce.
   WEB:  http://low-priority.appspot.com/ollydumpex/
   MAIL: lowprio20/_at_/gmail/_dot_/com

