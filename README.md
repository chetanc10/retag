# retag
Bash shell wrapper for cscope and ctags with disk and time friendly improvements for C-language based projects like linux-kernel.

# Installation
```basherbee install chetanc10/retag```  

# Features
- Directory exclusion:  
  Specific directories could be excluded using -x option saving time and disk-space.
- Kernel DB build:  
  Developers usually work on a single platform at a time with a kernel-clone, such cases don't need to include other platform code for scoping code. Using -k, users could select specific platform.  
  Also, retag automatically tries to remove some unwanted folders like Documentation, scripts, etc. However, user is prompted to choose if removing such folders from DB build.
  Additional to -k, user can also exclude other directories using -x
- Verbose DB build-time and size logs:
  -v option enables verbose logs to display total DB build-time and size, helps compare different retag runs with -k/-x//-xi on a source directory
- detag:
  An alias that removes all cscope, ctags and retag files from current directory
- Reduced runtime cluttered view:
  -k/-x/-xi can reduce redefined symbols in DB, thus reducing runtime cluttered view of redefined symbols.

# Examples
```retag```
- If ```.retag.files``` file is present and builds csccope/ctags DB using the files listed in ```.retag.files```
- Otherwise, it effectively does ```cscope -Rb &; ctags -R```

```retag -v```  
- Same as above, but additionally enables verbose mode to show the DB size and DB generation time

```retag -k arm64 -x drivers/gpu sound```  
- Excludes all arch/* subfolders except arch/arm64, excludes folders drivers/gpu and sound, creates fresh ```.retag.files``` and then creates cscope/ctags DB using the freshly generated ```.retag.files```  
- After this command, further retag invocations automatically detect ```.retag.files``` (unless detag deletes the file) to build DB, so user needs to give this retag with folder exclusion arguments just once per source until a ```detag```.

```retag -x drivers/gpu sound -xi arch/arm64```  
- Effectively same as the above.
- '-k' is provided to draw attention to the way retag could be used to simplify cscope/ctags build using retag.
