# Building android-ia source code
To build android-ia source you could use this link below:
https://github.com/android-ia/manifest/wiki
but you may face with some issues so this document is here to help.

# Java Development Kit
You have to use OpenJDK 8 to build source successfully if you use other versions or use Oracle Java Development Kit you get some error about it.

# Broken Makefile
Sometimes Makefiles have some issues like tab and spaces compilimation and they cuase to stop the build process.
In this cases feel free to look over the broken Makefile and sometimes you can change it!
Beleive me or not Makefile isn't rocket science and you could change it in some cases.
in this source a specific Makefile in this path:  
```kernel/android_ia/arch/x86/Makefile```
has tab and spaces issues in line no 178, if you take a look over it you will find this code:    
```
# GCC ignores '-maccumulate-outgoing-args' when used with '-Os'.
# If '-Os' is enabled, disable it and print a warning.
ifdef CONFIG_CC_OPTIMIZE_FOR_SIZE
        undefine CONFIG_CC_OPTIMIZE_FOR_SIZE
          $(warning Disabling CONFIG_CC_OPTIMIZE_FOR_SIZE.  Your compiler does not have -mfentry so you cannot optimize for size with CONFIG_FUNCTION_GRAPH_TRACER.)
endif
```
you can change it in right way but I can not so I simply comment it to be ignore in build process because this code almost generate a warning.

# Missing Binaries
You may face with some errors like this:
``` some-sort-of-binary-file command not found```
first you have to be sure that all the requirments are installed on your machine for more information see below link:  
https://source.android.com/source/initializing.html  
Althogh you installed all the requirments packages you get that error again.  
The source code released with required binaries to build under `prebuilts` directory so in this cases use `find ./prebuilts | grep some-sort-of-binary-file` to search among prebuilt binary files and after that add the path to `PATH` environment variable simply by typing:  
``` PATH=/path/to/binary/directory:$PATH ```  
or manully add the path to PATH variable in `/etc/environment` and after that type `source /etc/environment` 


# Missing Requirement
There is one requirment package that was not in mentioned in official documents and it breaks the build process simply install it on ubuntu machine by:  
```apt install genisoimage```

