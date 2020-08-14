# zsh

---

### Usage:

---

```
zsh [<options>] [<argument> ...]
```

---

### Special options:

---

-  `--help`     show this message, then exit
-  `--version`  show zsh version number, then exit
-  `-b`         end option processing, like --
-  `-c`         take first argument as a command to execute
-  `-o OPTION`  set an option by name (see below)

---

Normal options are named.  An option may be turned on by
`-o OPTION`, `--OPTION`, `+o no_OPTION` or `+-no-OPTION`.

---  

An option may be turned off by 
`-o no_OPTION', `--no-OPTION', `+o OPTION' or `+-OPTION'.

---

Options are listed below only in
`--OPTION` or `--no-OPTION` form.

---

### Named options:

---

- `--aliases`
- `--aliasfuncdef`
- `--allexport`
- `--alwayslastprompt`
- `--alwaystoend`
- `--appendcreate`
- `--appendhistory`
- `--autocd`
- `--autocontinue`
- `--autolist`
- `--automenu`
- `--autonamedirs`
- `--autoparamkeys`
- `--autoparamslash`
- `--autopushd`
- `--autoremoveslash`
- `--autoresume`
- `--badpattern`
- `--banghist`
- `--bareglobqual`
- `--bashautolist`
- `--bashrematch`
- `--beep`
- `--bgnice`
- `--braceccl`
- `--bsdecho`
- `--caseglob`
- `--casematch`
- `--cbases`
- `--cdablevars`
- `--cdsilent`
- `--chasedots`
- `--chaselinks`
- `--checkjobs`
- `--checkrunningjobs`
- `--clobber`
- `--combiningchars`
- `--completealiases`
- `--completeinword`
- `--continueonerror`
- `--correct`
- `--correctall`
- `--cprecedences`
- `--cshjunkiehistory`
- `--cshjunkieloops`
- `--cshjunkiequotes`
- `--cshnullcmd`
- `--cshnullglob`
- `--debugbeforecmd`
- `--dvorak`
- `--emacs`
- `--equals`
- `--errexit`
- `--errreturn`
- `--evallineno`
- `--exec`
- `--extendedglob`
- `--extendedhistory`
- `--flowcontrol`
- `--forcefloat`
- `--functionargzero`
- `--glob`
- `--globalexport`
- `--globalrcs`
- `--globassign`
- `--globcomplete`
- `--globdots`
- `--globstarshort`
- `--globsubst`
- `--hashcmds`
- `--hashdirs`
- `--hashexecutablesonly`
- `--hashlistall`
- `--histallowclobber`
- `--histbeep`
- `--histexpiredupsfirst`
- `--histfcntllock`
- `--histfindnodups`
- `--histignorealldups`
- `--histignoredups`
- `--histignorespace`
- `--histlexwords`
- `--histnofunctions`
- `--histnostore`
- `--histreduceblanks`
- `--histsavebycopy`
- `--histsavenodups`
- `--histsubstpattern`
- `--histverify`
- `--hup`
- `--ignorebraces`
- `--ignoreclosebraces`
- `--ignoreeof`
- `--incappendhistory`
- `--incappendhistorytime`
- `--interactive`
- `--interactivecomments`
- `--ksharrays`
- `--kshautoload`
- `--kshglob`
- `--kshoptionprint`
- `--kshtypeset`
- `--kshzerosubscript`
- `--listambiguous`
- `--listbeep`
- `--listpacked`
- `--listrowsfirst`
- `--listtypes`
- `--localloops`
- `--localoptions`
- `--localpatterns`
- `--localtraps`
- `--login`
- `--longlistjobs`
- `--magicequalsubst`
- `--mailwarning`
- `--markdirs`
- `--menucomplete`
- `--monitor`
- `--multibyte`
- `--multifuncdef`
- `--multios`
- `--nomatch`
- `--notify`
- `--nullglob`
- `--numericglobsort`
- `--octalzeroes`
- `--overstrike`
- `--pathdirs`
- `--pathscript`
- `--pipefail`
- `--posixaliases`
- `--posixargzero`
- `--posixbuiltins`
- `--posixcd`
- `--posixidentifiers`
- `--posixjobs`
- `--posixstrings`
- `--posixtraps`
- `--printeightbit`
- `--printexitvalue`
- `--privileged`
- `--promptbang`
- `--promptcr`
- `--promptpercent`
- `--promptsp`
- `--promptsubst`
- `--pushdignoredups`
- `--pushdminus`
- `--pushdsilent`
- `--pushdtohome`
- `--rcexpandparam`
- `--rcquotes`
- `--rcs`
- `--recexact`
- `--rematchpcre`
- `--restricted`
- `--rmstarsilent`
- `--rmstarwait`
- `--sharehistory`
- `--shfileexpansion`
- `--shglob`
- `--shinstdin`
- `--shnullcmd`
- `--shoptionletters`
- `--shortloops`
- `--shwordsplit`
- `--singlecommand`
- `--singlelinezle`
- `--sourcetrace`
- `--sunkeyboardhack`
- `--transientrprompt`
- `--trapsasync`
- `--typesetsilent`
- `--unset`
- `--verbose`
- `--vi`
- `--warncreateglobal`
- `--warnnestedvar`
- `--xtrace`
- `--zle`

---

#### Option aliases:
---

- `--braceexpand`            equivalent to `--no-ignorebraces`
- `--dotglob`                equivalent to `--globdots`
- `--hashall`                equivalent to `--hashcmds`
- `--histappend`             equivalent to `--appendcreate`
- `--histexpand`             equivalent to `--badpattern`
- `--log`                    equivalent to `--no-histnofunctions`
- `--mailwarn`               equivalent to `--mailwarning`
- `--onecmd`                 equivalent to `--singlecommand`
- `--physical`               equivalent to `--cdsilent`
- `--promptvars`             equivalent to `--promptsubst`
- `--stdin`                  equivalent to `--shinstdin`
- `--trackall`               equivalent to `--hashcmds`

---

#### Option letters:
---

- `-0`    equivalent to `--completeinword`
- `-1`    equivalent to `--printexitvalue`
- `-2`    equivalent to `--no-autoresume`
- `-3`    equivalent to `--no-nomatch`
- `-4`    equivalent to `--globdots`
- `-5`    equivalent to `--notify`
- `-6`    equivalent to `--beep`
- `-7`    equivalent to `--ignoreeof`
- `-8`    equivalent to `--markdirs`
- `-9`    equivalent to `--autocontinue`
- `-B`    equivalent to `--no-bashrematch`
- `-C`    equivalent to `--no-checkjobs`
- `-D`    equivalent to `--pushdtohome`
- `-E`    equivalent to `--pushdsilent`
- `-F`    equivalent to `--no-glob`
- `-G`    equivalent to `--nullglob`
- `-H`    equivalent to `--rmstarsilent`
- `-I`    equivalent to `--ignorebraces`
- `-J`    equivalent to `--appendhistory`
- `-K`    equivalent to `--no-badpattern`
- `-L`    equivalent to `--sunkeyboardhack`
- `-M`    equivalent to `--singlelinezle`
- `-N`    equivalent to `--autoparamslash`
- `-O`    equivalent to `--continueonerror`
- `-P`    equivalent to `--rcexpandparam`
- `-Q`    equivalent to `--pathdirs`
- `-R`    equivalent to `--longlistjobs`
- `-S`    equivalent to `--recexact`
- `-T`    equivalent to `--cbases`
- `-U`    equivalent to `--mailwarning`
- `-V`    equivalent to `--no-promptcr`
- `-W`    equivalent to `--autoremoveslash`
- `-X`    equivalent to `--listtypes`
- `-y`    equivalent to `--menucomplete`
- `-Z`    equivalent to `--zle`
- `-a`    equivalent to `--allexport`
- `-d`    equivalent to `--no-globalrcs`
- `-e`    equivalent to `--errexit`
- `-f`    equivalent to `--no-rcs`
- `-g`    equivalent to `--histignorespace`
- `-h`    equivalent to `--histignoredups`
- `-i`    equivalent to `--interactive`
- `-k`    equivalent to `--interactivecomments`
- `-l`    equivalent to `--login`
- `-m`    equivalent to `--monitor`
- `-n`    equivalent to `--no-exec`
- `-p`    equivalent to `--privileged`
- `-r`    equivalent to `--restricted`
- `-s`    equivalent to `--shinstdin`
- `-t`    equivalent to `--singlecommand`
- `-u`    equivalent to `--no-unset`
- `-v`    equivalent to `--verbose`
- `-w`    equivalent to `--cdsilent`
- `-x`    equivalent to `--xtrace`
- `-y`    equivalent to `--shwordsplit`

---