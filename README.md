# this is manual for install pysqlcipher3 for win 10
### VERSIONS
sqlcipher 4.4.2

pysqlcipher3 1.0.3

### Install tlc (i'm use 8.6)
https://www.activestate.com/products/tcl/downloads/  
#### (tclsh*.exe) is available in the PATH.(tclsh C:\Tcl\bin\tclsh.exe)



### Install VISUAL STUDIO (add) and VISUAL STUDIO C++ Build



### Install OpenSSL x64 or x32 (i'm use x64)
https://slproweb.com/products/Win32OpenSSL.html


##### add to PATH
###### x64
OPENSSL_CONF C:\Program Files\OpenSSL-Win64\bin\openssl.cfg
###### x32
OPENSSL_CONF C:\Program Files(x86)\OpenSSL-Win32\bin\openssl.cfg
######
### in folder 
C:\Program Files\OpenSSL-Win64\lib
#### save copy 
libcrypto.def and libcrypto.lib 
#### and rename at 
libeay32.def and libeay32.lib 

#### save copy
libssl.def and libssl.lib 
#### and rename at 
ssleay32.def and ssleay32.lib

######
### copy folder 
C:\Program Files\OpenSSL-Win64\include\openssl 
### to 
C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\VC\Tools\MSVC\14.28.29333\include





## Download sqlcipher
https://github.com/sqlcipher/sqlcipher

### in root sqlcipher change Makefile.msc



    TCC = $(TCC) -DSQLITE_TEMP_STORE=1 
    change to
    TCC = $(TCC) -DSQLITE_TEMP_STORE=2 -DSQLITE_HAS_CODEC -I"C:\Program Files\OpenSSL-Win64\include"
    
    ###############################################################################
    # If ICU support is enabled, add the linker options for it.
    #
    !IF $(USE_ICU)!=0
    LTLIBPATHS = $(LTLIBPATHS) /LIBPATH:$(ICULIBDIR)
    LTLIBS = $(LTLIBS) $(LIBICU)
    !ENDIF
    # <</mark>>
    # You should not have to change anything below this line
    ###############################################################################

    change to

    ###############################################################################
    # If ICU support is enabled, add the linker options for it.
    #
    !IF $(USE_ICU)!=0
    LTLIBPATHS = $(LTLIBPATHS) /LIBPATH:$(ICULIBDIR)
    LTLIBS = $(LTLIBS) $(LIBICU)
    !ENDIF
    # <</mark>>

    LTLIBPATHS = $(LTLIBPATHS) /LIBPATH:"C:\Program Files\OpenSSL-Win64\lib\VC\static"
    LTLIBS = $(LTLIBS) libcrypto64MT.lib libssl64MT.lib ws2_32.lib shell32.lib advapi32.lib gdi32.lib user32.lib crypt32.lib


    # You should not have to change anything below this line
    ###############################################################################


### x64 Native Tools Command (VS)
    path\to\sqlcipher>
    
    nmake /f Makefile.msc clean
    nmake /f Makefile.msc



## Download pysqlcipher3
https://github.com/rigglemania/pysqlcipher3
### create folder /amalgamation in /pysqlcipher3

#### COPY TWO FILES FROM /sqlcipher
sqlite3.c sqlite3.h
#### TO /pysqlcipher3/amalgamation

## Download sqlite-amalgamation
https://sqlite.org/download.html

my version https://sqlite.org/2021/sqlite-amalgamation-3340100.zip

### create folder 
/pysqlcipher3/src/python3/sqlcipher

### copy 4 files from sqlite-amalgamation-3340100.zip  
shell.c sqlite3.c sqlite.h sqliteext.h
### to 
/pysqlcipher3/src/python3/sqlcipher	

### x64 Native Tools Command (VS)
    path\to\pysqlcipher3>

    setup.py clean  

    setup.py build_amalgamation

    setup.py install

maybe this help u
