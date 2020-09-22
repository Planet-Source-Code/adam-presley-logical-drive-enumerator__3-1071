<div align="center">

## Logical Drive Enumerator


</div>

### Description

This code enumerates a list of the logical drive letters recognized by Windows, and displays this list in a message box.
 
### More Info
 
This code works only in Win32 enviornment.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Adam Presley](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/adam-presley.md)
**Level**          |Beginner
**User Rating**    |4.0 (12 globes from 3 users)
**Compatibility**  |C, Microsoft Visual C\+\+, Borland C\+\+
**Category**       |[System Services/ Functions](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/system-services-functions__3-23.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/adam-presley-logical-drive-enumerator__3-1071/archive/master.zip)

### API Declarations

```
#include <windows.h>
#include <string.h>
```


### Source Code

```
WINAPI WinMain(HINSTANCE hInstance, HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nCmdShow)
{
  DWORD Drives;
  char output[255];
  DWORD bit_modify[] = {
   1, 2, 4, 8, 0x10, 0x20, 0x40, 0x80, 0x100, 0x200,
   0x400, 0x800, 0x1000, 0x2000, 0x4000, 0x8000, 0x10000,
   0x20000, 0x40000, 0x80000, 0x100000, 0x200000, 0x400000,
   0x800000, 0x1000000, 0x2000000
  };
  char *drive_list[] = {
   "A: ", "B: ", "C: ", "D: ", "E: ", "F: ", "G: ", "H: ", "I: ",
   "J: ", "K: ", "L: ", "M: ", "N: ", "O: ", "P: ", "Q: ",
   "R: ", "S: ", "T: ", "U: ", "V: ", "W: ", "Y: ", "Z: "
  };
  // ---- Clear the output buffer ----
  strcpy(output, "");
  // ---- Now, get the drives ----
  Drives = GetLogicalDrives();
  if(Drives == 0) {
   MessageBox(NULL, "There was an error getting the list of logical drives.",
         "Error!", MB_OK|MB_ICONERROR);
   return -1;
  }
  // ---- Create the list in the variable 'output' ----
  for(int loop = 0; loop < 25; loop++)
   if(Drives & bit_modify[loop]) strcat(output, drive_list[loop]);
  MessageBox(NULL, output, "Drives List...", MB_OK|MB_ICONINFORMATION);
  return 0;
}
```

