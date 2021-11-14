# Change Log

Use `R()` to rename if I change a label.

## 03/21/17 03:11:37
 - N/A

## 03/17/17 00:35:11
  - Added toggle AutoSave `<CTRL-SHIFT-s>`.

##  03/14/17 00:14:39
  - TempleOS version 5.03 Released
  ```holyc
  R("pen_width","thick");
  ```
##  02/05/17 16:37:39
  - Added [BlkChain.DD](./BlkChain.md).

##  02/03/17 17:27:36
  - Added multicore [AMathODE.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/AMathODE.HC).
  - Improved support for sub and super scripts.

##  01/31/17 10:22:10
  - Added [LightTable.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/LightTable.HC).
  - Added [TOS Linux Setup](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/AcctExample/TOS/TOSPolicies.DD)

##  01/27/17 08:13:37
  - Added `DocLineRead()` and `DocLineWrite()`.

##  01/25/17 20:44:17
  ```holyc
  R("DocLineNumGoto","DocGoToLine");
  R("Clipboard","Clip");
  R("AutoMountIDE","MountIDEAuto");
  R("ChgExt","ExtChg");
  R("DftExt","ExtDft");
  R("CurDir","DirCur");
  R("MkDir","DirMk");
  R("ChkDsk","DskChk");
  R("ChgDsk","DskChg");
  R("PrtDsk","DskPrt");
  R("RBlks","BlkRead");
  R("WBlks","BlkWrite");
  R("FRBlks","FBlkRead");
  R("FWBlks","FBlkWrite");
  R("Cluster","Clus");
  R("RClusters","ClusRead");
  R("WClusters","ClusWrite");
  ```

## 01/24/17 21:56:06
  - Improved [JukeBox.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/Psalmody/JukeBox.HC)
  - Added `DocTreeWrite()` and `DocTreeAppend()`.
  ```holyc
  R("TreeBranch","Tree");
  ```
## 01/22/17 06:08:00
  - TempleOS version 5.02 Released
  - Changed polling of `KbdMsHndlr()` in `WinMgrSleep()`, increased fifos.

## 01/17/17 18:11:53
  - Fixed class offset so `#assert`'s don't lag a token.

## 01/17/17 14:39:41
  - Added `blkdev.ins_base0`[^1] and `blkdev.ins_unit`[^1].
  - Added make `RedSeaISO()` to `FileMgr()`.
  - Added `blkdev.dft_iso_c_filename`[^1]

## 01/17/17 06:12:21
  ```holyc
  R("MIN_...","..._MIN");
  R("MAX_...","..._MAX");
  R("NUM_...","..._NUM");
  ```
## 01/14/17 19:16:51
  - Created [TOS](https://github.com/cia-foundation/TempleOS/tree/archive/Demo/AcctExample/TOS).
  ```holyc
  R("MAX_...","_NUM...");
  ```
## 01/14/17 09:43:12
  - Improved [TOSHolySpirit.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/AcctExample/TOS/TOSHolySpirit.HC).
  - Added ["cmp U0 Expression" warn](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Compiler/PrsExp.HC).
  - Improved syntax highlighting.

## 01/11/17 03:33:33
  - TempleOS version 5.01 Released
  - Added show mouse pos to `<CTRL-ALT-G>`.
  - Improved `TOSRegen()`.
  - Added `Let2Let()`.
  ```holyc
  R("ChangeLog","ChgLog");
  ```
## 01/10/17 14:27:58
  - Made `DocPut()` use parent task's doc if input filter task.
  - Added `Once()`, `AOnce()`, `OnceFlush()`, `AOnceFlush()`, `OnceDrv()`, `AOnceDrv()` and `OnceExe()`.
  - Added `RegAppend()` and `RegCnt()`;
  ```holyc
  R("RegSetDftEntry()","RegDft()");
  R("RegExeBranch()","RegExe()");
  R("RegWriteBranch()","RegWrite()");
  R("DoOnce","Once");
  ```
## 01/10/17 11:45:41
  - Added [InsReg.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/InsReg.HC) with `InsReg()`, `InsRereg()` and `InsUnreg()`.
  - Added [Host.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Host.HC) with `HostChgDsk()`.
  - Added [TOS.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Utils/TOS.HC) with `TOSStdIns()`.
  - Added cmd line args for partition % to `DskPrt()`.

## 01/09/17 21:48:34
  ```holyc
  R("a1","arg1");
  R("a2","arg2");
  R("r","res");
  ```
## 01/09/17 02:30:59
  - Improved compiler `ICSlashOp()`.
  - Added `Panic()`.
  - Made it possible to mount just one partition.
  - Fixed creation of RedSea ISOs.
  - Organized [PersonalMenu.DD](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/PersonalMenu.DD).
  - Moved AfterEgypt to the supplemental disk.

## 01/06/17 06:07:19
  - Fixed `DskChg()`.
  - Improved [OSTestSuite.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Misc/OSTestSuite.HC).

## 01/05/17 04:53:21
  - No longer support ASCII#12, `<CTRL-l>` CH_FORM_FEED.
  - Fixed `sys_var_init_flag`[^2].
  - `GRScrnCaptureRead()`.

## 01/04/17 18:06:14
  - Added [TOSPolicies.DD](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/AcctExample/TOS/TOSPolicies.DD).
  - Got rid of `mouse.throttle`. 
  - Improved `MemRep()`.
  - Changed [WallPaper.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/WallPaper.HC).
  ```holyc
  R("Button","Bttn");
  R("Handler","Hndlr");
  R("InputPointer","Mouse");
  R("U0 pad;",";"); // For align `#asserts`
  ```
  
## 01/03/17 12:23:49
  - Added chk for [TOSMisc.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/AcctExample/TOS/TOSMisc.HC).
  - Improved [TOSDistro.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/AcctExample/TOS/TOSDistro.HC).
  - Removed TempleOSBooks1.ISO TempleOSBooks2.ISO out of http://www.templeos.org/TempleOSSup1.ISO.
  ```holyc
  R("chars_cmp...","char_bmp...");
  ```
  
## 01/01/17 17:16:16
  - TempleOS version 5.00 Released
  - Added `Collapse()`.
  - Added `CursorRem()`.

## 12/31/16 07:21:20
  - Added `MemPageRep()`.
  ```holyc
  R("SYS_SEMA_...","SEMA_...");
  R("SYSf_CTRL_ALT_...","CTRL_ALT_...");
  R("ThrowBreak()","Break()");
  ```
  
## 12/30/16 23:42:20
  - Overhauled [PageTables.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/Mem/PageTables.HC).
  ```holyc
  R("Pages512","Pags");
  R("BusyWait()","Busy()");
  ```
  
## 12/29/16 10:21:44
  - Changed `Snd()` from freq to a I8 val called an ona.
  - Fixed err in music octaves.
  - To convert songs, download Supplemental#1 ISO from the AppStore on http://www.templeos.org and run [Sup1/Sup1Utils/CvtSong500.HC]().
  
## 12/22/16 16:18:32
  ```holyc
  R("CSrvCmd","CJob");
  R("CSrvCtrl","CJobCtrl");
  ```

## 12/03/16 13:19:58
  - Improved [Talons.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Talons.HC).
  ```holyc
  R("SpriteMat3B()","Sprite3Mat4x4B()");
  R("SpriteX3B()","Sprite3XB()");
  R("SpriteY3B()","Sprite3YB()");
  R("SpriteZ3B()","Sprite3ZB()");
  ```

## 12/03/16 10:16:26
  - Changed `__CMD_LINE__`.
  - Added CProgress.tf.
  - Added `sys_staff_mode_flag`[^3].
  ```holyc
  R("except_caller","except_callers");
  ```
  
## 11/30/16 22:44:35
  - Added `SpriteTransform()`.

## 11/28/16 07:11:41
  - Improved [Titanium.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/Titanium/Titanium.HC).

## 11/26/16 22:43:51
  - Added solar storms to [X-Caliber.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/X-Caliber/X-Caliber.HC).
  ```holyc
  R("TimeOut","Titanium");
  ```
  
## 11/20/16 19:46:43
  - TempleOS version 4.13 Released
  - Improved [Titanium.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/Titanium/Titanium.HC).
  - Improved [X-Caliber.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/X-Caliber/X-Caliber.HC).

## 11/19/16 08:19:51
  - Improved Budget application.

## 11/17/16 18:49:51
  - Improved [RocketScience.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/RocketScience.HC).
  - Improved [Rocket.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Rocket.HC).
  ```holyc
  R("EagleDive","Talons");
  ```
  
## 10/28/16 05:54:27
  - Added [RadixSort.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/RadixSort.HC).

## 10/26/16 00:21:06
  - Added CProgress.t0[^4].
  - Improved [Boot.DD](./Boot.md).

## 10/25/16 18:02:44
  - Improved [SpriteEd.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Gr/SpriteEd.HC).
  - Improved [TOSHolySpirit.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/AcctExample/TOS/TOSHolySpirit.HC).

## 10/12/16 10:55:26
  - Added `CCF_NO_CHAR_CONST`[^5].
  - Improved [ToHtml.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/ToHtmlToTXTDemo/ToHtml.HC).

## 10/03/16 01:09:35
  - Changed `GodWord()`.

## 09/30/16 18:29:59
  - Improved `Rand()`'s.
  - Improved [ToTXT.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/Opt/Utils/ToTXT.HC).

## 09/29/16 10:13:14
  - TempleOS version 4.12 Released
  - Added `TASKf_CMD_LINE_PMT`[^6].
  - Improved `TaskWait()`.
  - Improved `DeathWait()`.

## 09/27/16 12:40:21
  - Added `SndRst()`.
  - Got rid of crappy reverb in [PsalmodyMain.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/Psalmody/PsalmodyMain.HC).

## 09/27/16 11:09:25
  - Improved [OSTestSuite.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Misc/OSTestSuite.HC).
  - Fixed bug in `EdCharIns()` printing $$ cmds.
  - Added `FUF_JUST_DD`[^7] and `FILEMASK_DD`[^8].

## 09/27/16 01:05:52
  - Improved [MemOverview.DD](./MemOverview.md).
  - Got rid of `/Demo/Lectures/Mem`.
  - Made filename paths relative to document location in DolDoc links.
  ```holyc
  R("Temp","Tmp");
  ```

## 09/26/16 00:44:42
  - Added CloseAssault and OverRun to [ToTheFront.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/ToTheFront/ToTheFront.HC).

## 09/22/16 07:53:20
  - Improved [Box.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/Box.HC).
  - Improved [SpritePlot3D.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Graphics/SpritePlot3D.HC).

## 09/21/16 17:09:40
  - Fixed bug in [BomberGolf.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/BomberGolf.HC).

## 09/20/16 15:57:30
  - Improved [Boot.DD](./Boot.md).
  ```holyc
  R("Screen","Scrn");
  R("WinMgrSync","Refresh");
  R("InDbg","DbgMode");
  ```

## 09/20/16 07:31:52
  ```holyc
  R("DAT","DATA");
  R("Auto","In");
  R("AutoStr","InStr");
  R("AutoFile","InFile");
  R("AUT","IN");
  R("GRA","GR");
  ```
## 09/18/16 20:40:44
  - Added [WhyNotMore.DD](./WhyNotMore.md).

## 09/18/16 12:52:03
  - TempleOS version 4.11 Released
  - Fixed bug in `IsDotC()`.
  ```holyc
  R("CPP","HC");
  R("HPP","HH");
  R("TXT","DD");
  ```

## 09/06/16 13:01:42
  - Added `OPTf_WARN_HEADER_MISMATCH`[^9].
  - Changed `WinInside()`.
  - Got rid of `MSG_FOCUS`, `MSG_MOVE`, and `MSG_SIZE`. There are no longer messages for moving and sizing windows.

## 09/06/16 02:40:43
  - Improved [MagicPairs.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/MagicPairs.HC).

## 08/27/16 09:45:39
  - Improved `CPURep()`.
  - Improved [OSTestSuite.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Misc/OSTestSuite.HC).
  - Added `DeathWait()`.

## 08/22/16 04:14:47
  ```holyc
  R("TK_DOT_DOT_DOT","TK_ELLIPSIS");
  ```

## 07/17/16 13:03:12
  - Improved `DocOpt()`.

## 07/17/16 03:23:53
  - Improved [RawHide.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/RawHide.HC).

## 07/15/16 10:11:10
  - TempleOS version 4.10 Released
  - Improved [Talons.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Talons.HC).

## 07/15/16 05:17:24
  - Created `CDevGlbls.uncached_alias`[^10].
  - Added 1 Gig page table support.

## 07/13/16 17:21:19
  - Added multicore report to `CPURep()`.

## 07/09/16 08:46:36
  - Changed scoring in [Talons.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Talons.HC).
  - Replaced many "%Q" with "%$Q".
  - Fixed '\x24'.
  - Added '\d' for '$'.

## 07/08/16 14:30:19
  - Fixed `REP_STOSB` and `MemSet()` for 64-bit.
  ```holyc
  R("root","head");
  ```

## 07/07/16 07:21:03
  - `DocRead()` changes to file's dir so relative filenames work.
  - Added AppStore to website with Supplemental#1 ISO for download.

## 07/06/16 23:45:30
  - Fixed multicore bug in `Sprite3()`.
  - Improved [Talons.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Talons.HC).

## 07/05/16 06:03:47
  - TempleOS version 4.09 Released
  - Improved [Talons.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Talons.HC).
  - Improved `GrFillTri0()`.

## 07/03/16 04:30:05
  - Added `Unmount()`.
  - Made BootLoader mandatory in `RedSeaISO()`.
  - Added `BDT_ISO_FILE_READ`[^11].

## 07/01/16 05:29:08
  - Made underscore mandatory on [HolyC](./HolyC.md) callable asm functions.

## 06/28/16 13:15:08
  - Changed `MemRep()`.
  - Changed [WallPaper.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Adam/WallPaper.HC).

## 06/26/16 14:01:16
  - Added `PopUpRunFile()`.
  - Made boot code modular.

## 06/24/16 14:15:13
  - Added A.I. to [KeepAway.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Apps/KeepAway/KeepAway.HC) and changed scoring.

## 06/24/16 02:55:42
  - TempleOS version 4.08 Released
  - Added Polygon, Fence, Prism and ResetColor commands to `SpriteMeshEd()`.
  ```holyc
  R("Reverse","Rev");
  R("Select","Sel");
  ```

## 06/23/16 01:03:36
  - Added `GrFillCircle()`.
  - Added `GrLineFat3()`.

## 06/18/16 16:16:22
  - Modified `KeyDevAdd()`.
  - Changed args to `PutFileLink()`.
  - Added `HomeSet()`. Added "~" as special directory designator.
  - Changed filename exclude mask char from '~' to '!'. See /Doc/FileUtils.DD.
  - Got rid of `/Home/HomePkgs.HC`.
  ```holyc
  R("nounusedwarn","no_warn");
  R("sub_switch_start","start");
  R("sub_switch_end","end");
  ```

## 06/16/16 20:59:41
  - `<CTRL-ALT-t>` is terminal window.
  - `<CTRL-ALT-n>` is next task.

## 06/16/16 19:49:39
  - Added [Comm.HC](./Comm.HC).
  - Added [StdTempleOSPC.DD](StdTempleOSPC.md).
  - Added [FontCyrillic.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Kernel/FontCyrillic.HC). `<CTRL-ALT-f>`

## 06/02/16 03:20:56
  - TempleOS version 4.07 Released
  - Added claws to [Talons.HC](https://github.com/cia-foundation/TempleOS/blob/c26482bb6ad3f80106d28504ec5db3c6a360732c/Demo/Games/Talons.HC).

[^1]: See MN:CBlkDevGlbls

[^2]: See MN:sys_var_init_flag

[^3]: See MN:sys_staff_mode_flag

[^4]: See MN:CProgres

[^5]: See MN:CCF_NO_CHAR_CONST

[^6]: See MN:TASKf_CMD_LINE_PMT

[^7]: See MN:FUF_JUST_DD

[^8]: See MN:FILEMASK_DD

[^9]: See MN:OPTf_WARN_HEADER_MISMATCH

[^10]: See MN:CDebGlbls

[^11]: See MN:BDT_ISO_FILE_READ
