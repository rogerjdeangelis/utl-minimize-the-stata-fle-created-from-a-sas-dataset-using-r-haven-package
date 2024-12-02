    %let pgm=utl-minimize-the-stata-fle-created-from-a-sas-dataset-using-r-haven-package;

    Minimize the stata fle created from a sas dataset  using r haven package

    github
    https://tinyurl.com/mwvueez7
    https://github.com/rogerjdeangelis/utl-minimize-the-stata-fle-created-from-a-sas-dataset-using-r-haven-package

     *___  _
    / ___|| |_ ___  _ __ __ _  __ _  ___
    \___ \| __/ _ \| `__/ _` |/ _` |/ _ \
     ___) | || (_) | | | (_| | (_| |  __/
    |____/ \__\___/|_|  \__,_|\__, |\___|
                              |___/
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*                               Size on Disk(bytes)                                                                      */
    /*                         R                                                                                              */
    /*            NUMBERS    CONVERSION       SAS          STATA                                                              */
    /*                                                                                                                        */
    /* 1 SAS 64bit floats    none           8,257,536    8,003,584 bytes                                                      */
    /*                                                                                                                        */
    /* 2                     as.integer       N/A        4,001,792                                                            */
    /*                                                                                                                        */
    /*           STRINGS                                                                                                      */
    /*                                                                                                                        */
    /* 3 SAS strings 4096    gets longest   1,114,112       12,288                                                            */
    /*                                                                                                                        */
    /**************************************************************************************************************************/


       CONTENTS

           1 numbers default
           2 converrt to integer
           3 strings

     Stata does have other formats but R does not support them yet

        1. byte (-127-127)
        2. 32bit floats
        3  strL and Str# (length)
        4  r does support thresholds


    Related repos
    github
    https://tinyurl.com/ykvxnvuy
    https://github.com/rogerjdeangelis/utl-sas-to-and-from-sqllite-excel-ms-access-spss-stata-using-r-packages-without-sas
    https://github.com/rogerjdeangelis/utl_importing_and_exporting_sas7bdats__without_sas

    /*                         _                        _       __             _ _
    / |  _ __  _   _ _ __ ___ | |__   ___ _ __ ___   __| | ___ / _| __ _ _   _| | |_
    | | | `_ \| | | | `_ ` _ \| `_ \ / _ \ `__/ __| / _` |/ _ \ |_ / _` | | | | | __|
    | | | | | | |_| | | | | | | |_) |  __/ |  \__ \| (_| |  __/  _| (_| | |_| | | |_
    |_| |_| |_|\__,_|_| |_| |_|_.__/ \___|_|  |___/ \__,_|\___|_|  \__,_|\__,_|_|\__|

    */

    /*--- input ---*/

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.havnum;
      do i=1 to 1000000;
        x=1
        output;
      end;
      drop i;
    run;quit;


    %utl_rbeginx;
    parmcards4;
    library(haven)
    library(float)
    havnum<-read_sas("d:/sd1/havnum.sas7bdat")
    str(havnum)
    write_dta(havnum, "d:/dta/havnum.dta")
    ;;;;
    %utl_rendx;

    d:/dta/havnum.dta  8,003,584

    /*___    _       _                             _________  _     _ _
    |___ \  (_)_ __ | |_ ___  __ _  ___ _ __ ___  |___ /___ \| |__ (_) |_
      __) | | | `_ \| __/ _ \/ _` |/ _ \ `__/ __|   |_ \ __) | `_ \| | __|
     / __/  | | | | | ||  __/ (_| |  __/ |  \__ \  ___) / __/| |_) | | |_
    |_____| |_|_| |_|\__\___|\__, |\___|_|  |___/ |____/_____|_.__/|_|\__|
                             |___/
    */

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.havnum;
      do i=1 to 1000;
        x=1;
        output;
      end;
      drop i;
    run;quit;

    %utl_rbeginx;
    parmcards4;
    library(haven)
    havnum<-read_sas("d:/sd1/havnum.sas7bdat")
    havnum$X <- as.integer(havnum$X)
    write_dta(havnum, "d:/dta/havnum.dta")
    ;;;;
    %utl_rendx;

    /*____       _        _
    |___ /   ___| |_ _ __(_)_ __   __ _ ___
      |_ \  / __| __| `__| | `_ \ / _` / __|
     ___) | \__ \ |_| |  | | | | | (_| \__ \
    |____/  |___/\__|_|  |_|_| |_|\__, |___/
                                  |___/
    */


    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.havchr;
    length x $1000;
      do i=1 to 1000;
        x='1234567890';
        output;
      end;
      drop i;
    run;quit;

    %utl_rbeginx;
    parmcards4;
    library(haven)
    library(float)
    havchr<-read_sas("d:/sd1/havchr.sas7bdat")
    write_dta(havchr, "d:/dta/havnum.dta")
    ;;;;
    %utl_rendx;


    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

