LIST.G4B v0.8 (20231003), by deomsh
Function:  Wildcards '?'/ '*' in file names for ls; sort/ redirect/ pipe/ CMD
Use 1:     LIST.G4B [switches] FILE
Use 2:     LIST.G4B [-me] [switches] [DEVICE]PATH*.EXT1 [*.EXT2] [*.EXT...]
Use 3:     LIST.G4B [-md] [switches] [DEVICE]PATH[:]DIR1[*]/ [[:]DIR...[*]/]
Use 4:     LIST.G4B [-ms] [switches] [DEVICE]PATH [:][SUB1][*]/] [[:]SUB..[*]/]
Use 5:     LIST.G4B [switches] FILE ">" "FILE2"
Use 6:     LIST.G4B [switches] FILE "|" "TARGET" [VAR:varname]
Use 7:     LIST.G4B [switches] FILE CMD "CMD1" ["CMD2"] ["CMD3"] ... ["CMD8"]
Use 8:     LIST.G4B [/?|-?]
Switches:  [-mdbase:sector] [-case] [-sfn|--sfn] [-b|-l|-lh|-w|-c] [-d|-f] [-s]
           [-e|--e] [-o[g|-g]n|-n|e|-e|s|-s] [-qs]] [-q] [-col:NXDES]
           [-m[n]:FILEx]
Wildcards: ? and * before, inside, after part of file name/ extension/ combined
Wildcards: one * at the end of the last directory in path allowed too
Switches:
Not case-sensitive and: order is free IF before FILE
Single qoutes textual only, never used; default file names not case sensitive
'-mdbase:startsector' max 0x7FEFFF (default 0x3000), must end on 1000-7FFF
 if below/ above range: mdbase is changed with +0x1000/ +0x2000
'-case' case-sensitive (with -on|-o-n|-ox|-o-x uppercase will come first/ last)
'-sfn'/ '--sfn' 8+3 file or folder names/ Long Files Names only
'-b' long list, OR '-l' long list with filesize, OR '-lh' same in KB, MB or GB
 OR '-w' list for wide list (graphicsmode decides number of columns: 5-12) OR
'-c' list for column list (graphicsmode decides number of columns: 5-12)
'-d' output: directories only, OR '-f' output: files only
'-e'/ '--e' output empty/ not-empty folders (with '-d' no files)
'-o[g|-g]n|-n|e|-e|s|-s]' for sorting (order after '-o' is free)
'-og' sort output: directories first, OR '-o-g' sort output: files first
'-o[g|-g]n'/ '-o[g|-g]e' sort on name/ extension: a-z OR '-n'/ '-e' sort: z-a
 OR '-o[g|-g]s'/ '-o[g|-g]-s' sort on filesize: low-high/ high-low
'-qs' force 'quick sort' instead of 'selection sort' (not used for 'g'/ '-g')
'-q' fully quiet, exports set-variable 'COUNT': folder, files, total bytes
'-s' parse sub-directories (with '-sfn': 8+3 only)
'-col:NXDES' 5 numbers needed: 1-F; colors: N=file name, X=file extension
      D=not-empty directory, E=empty directory, S=sub-directory (for '-s')
 Default 'colors': 77F87 (white, white, highlighted, grey, white)
 To get color numbers use second number found with 'echo -h' (background black)
 Instead '-col:NXDES' variable 'lscol=NXDES' can be set before (always exported)
 Color of 'N' must be different from color(s) of 'DE'
'-m[n]:FILEx' parse image files or block device 'regions' with a File System
 'FILEx' must contain at least a full device, device in 'FILE' is ignored 
 With spaces use double quotes or escaped '\ ' spaces
 If mbr present, use partition number 'n' (n=0-63)
 If only 'device' is used, number of sectors will be estimated
 Max size depends of available memory
'-me' multiple extensions after FILE: must start with '*.' (max 100 extensions)
 With '-me' NO wildcards in extensions , in name-part of FILE still possible
'-md' parse multiple directories, one asterisk wildcard at the end allowed
 with ':' before: NOT parse. Always '/' needed afterwards OR
'-ms' parse multiple sub-directories, use PATH '/:/' to skip root - see '-md'
Both '-md'/ '-ms': use double qoutes if DIR's containing spaces (or use '\ ')
Both '-md'/ '-ms': use double qoutes if DIR's containing spaces (or use '\ ')
Remarks:
Compatible with grub4dos versions 20170607 and later, grub4efi recent versions
No memory used, except 0x3000+1 for '-sfn'; '-md' +0x100; sorting +0x1000
 With '-m[n]:FILEx' max available (top-)memory
Printing to screen can be interrupted by pressing 'Escape', ended with 'Q'
Default colors are like 'ls', but empty directories grey (see color-switch)
Compatible with actual status of pager (not autoswitching pager on!)
Wildcard '?' replaces ONE char in NAME/ EXT, wildcard '*' undefined number
 With wildcard '*' after NAME and without EXT all extensions included (like DIR)
 To get only file/ folder-names having extensions: use '.?*' for '.EXT'
Redirecting: ">" / piping: "|" - the double qoutes are mandatory!
 Redirecting to FILE2: if containing spaces, use escaped spaces '\ ' only
Piping: if targeting 'set VAR=' use "call set VAR=%^^^VAR% " VAR:VAR(name)
 Piping: VARnames are free EXCEPT 'vArZyXwV' and 'VaRzYxWv'
Functions piping and redirecting are not compatible with [-b|-l|-lh]
After CMD max 8 commands supported (in double qoutes) - watch use of '"' inside
Internal variables I: 'DEVICE', 'PATH', 'name', 'ext' and 'file' (all combined)
Internal variables II: 'filesize' and 'color': file => '$[]', folder => '$[0x0F]'
Use of internal variables: always with 'call' and TWO '^^' inside: '\x25^^var\x25'
In 'FILE': path is mandatory, at least '/' (current root)
 If FILE contains spaces, use double qoutes around, or escaped spaces: '\ '
Example: LIST.G4B /
Example: LIST.G4B /filename.ext
Example: LIST.G4B "(hd0,0)/Long Vfat File Name.Long Extension"
Example: LIST.G4B (hd0,0)/Long\ Vfat\ File\ Name.Long\ Extension
Example: LIST.G4B /*.g4b
Example: LIST.G4B -w /*.?*
Example: LIST.G4B /??t*.?*
Example: LIST.G4B /*f*a*?
Example: LIST.G4B -case (hd6,2)/EXT234/??T*.?*
Example: LIST.G4B -sfn /
Example: LIST.G4B -me (hd0,0)/*.txt *.g4b *.bat *.lst "*.E T"
Example: LIST.G4B -n -e -b /
Example: LIST.G4B -l /
Example: LIST.G4B -lh /
Example: LIST.G4B -og -s /
Example: LIST.G4B -on /
Example: LIST.G4B -o-g-n /
Example: LIST.G4B -oe -c (hd0,0)/WINDOWS/SYSTEM/
Example: LIST.G4B -c -on /
Example: LIST.G4B -col:BDE6F -w -ogn -s (hd0,0)/WINDOWS/
Example: LIST.G4B -l -os (hd0,0)/
Example: LIST.G4B -q -s / ;; echo \x25COUNT\x25
Example: LIST.G4B -m:(hd0,0)/FILENAME.IMG /
Example: LIST.G4B -m:(0xe0)26+720 -s /
Example: LIST.G4B -m0:(hd0,0)/MBRFILE.IMG /somedir/
Example: LIST.G4B -md (hd0,0)/WINDOWS/SYS*/ COMMAND/ :INF/ "START MENU/"
Example: LIST.G4B -ms (hd0,0)/WINDOWS/ SYS*/ IOSUBSYS/ :SYSTEM/
Example: LIST.G4B -ms -s (hd0,0)/:/ IOSUBSYS/ INF/ APP*/ START*/
Example: LIST.G4B -oe -l /F*.?*
Example: LIST.G4B "(hd0,0)/pro???? ?*"
Example: LIST.G4B "(hd0,0)/?at*.?* ">" (md)0x300+1
Example: LIST.G4B "(hd0,0)/?at* "|" "call set VAR1=%^^^VAR1% " VAR:VAR1
Example: LIST.G4B -d (hd0,0)/ "|" "echo -n $[0x00] $[0xDE]"
Example: LIST.G4B (hd0,0)/ CMD "call if %^^color%==$[] && call echo -n -e $[0x0E]%^^name%%%^^ext%  ! echo -n -e $[0xDE]%^^name%%%^^ext%$[0x00] "
Example: LIST.G4B -d --e (hd0,0)/ CMD "call echo $[0x09]%^^file%/ && call LIST.G4B -bs %^^file%/ && echo && debug msg=0"

History:
Version 0.8
Bugfix: redirect to '">" nul' ending with cat-error
Bugfix: not everything showed with '-ogn/-oge' combined with '-s'
Bugfix: echoing subdirectories if '-s' combined with CMD (without wildcards)
Bugfix: switches '-og' and '-f/-d' not compatible anymore
Bugfix: switch "-col:NXDES':  N and DE must be different
Bugfix: with '-e -d -s' if no empty dirs found
Bugfix: with '-w/-c' initial pager status not returned
Bugfix: Better fill-out with '-c'
New: always number of folders/files/total filesize afterwards
     except with '-w/-c': set variable 'COUNT' exported like '-q'
     switch '-n' removed, switch '-q' instead of '-nq'
New: Name starting with dot supported if no Extension exists (linux)
New 'File not found' if no folders/files found
New switch: '-m[n]:FILEx' to parse image files or block device 'regions' with a File System

Version 0.7 
First published verison
