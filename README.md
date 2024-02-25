# utl-when-the-same-variable-has-different-lengths-in-three-datasets-set-length-to-longest-length
When the same variable has different lengths in three datasets set length to longest length 
    %let pgm=utl-when-the-same-variable-has-different-lengths-in-three-datasets-set-length-to-longest-length;

    When the same variable has different lengths in three datasets set length to longest length

    github
    http://tinyurl.com/38p3jwzw
    https://github.com/rogerjdeangelis/utl-when-the-same-variable-has-different-lengths-in-three-datasets-set-length-to-longest-length


    Related repos

    https://github.com/rogerjdeangelis/utl-how-to-append-datasets-when-type-and-length-are-not-the-same
    https://github.com/rogerjdeangelis/utl-applying-a-template-to-set-common-table_names-labels-formats-and-lengths
    https://github.com/rogerjdeangelis/utl-how-to-get-rid-of-multiple-length-warnings-when-appending-tables
    https://github.com/rogerjdeangelis/utl-setting-the-length-of-character-variables-to-the-longest-lengths-before-joining-tables
    https://github.com/rogerjdeangelis/utl_append_tables_when_the_same_variables_have_different_types_and_lengths

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*                                |                                              |                                        */
    /*       INPUT                    |             PROCESS                          |         OUTPUT                         */
    /*                                |                                              |                                        */
    /* Data Set Name  WORK.Z1         |    data _null_;                              |  Data Set Name  WORK.Z1                */
    /* ======================         |                                              |  ======================                */
    /*  Variables in Creation Order   |      * get meta data about group;            |   Variables in Creation Order          */
    /*                                |      if _n_=0 then do;                       |                                        */
    /* #    Variable    Type    Len   |         %let rc=%sysfunc(dosubl('            |  #    Variable    Type    Len          */
    /*                                |             proc sql;                        |                                        */
    /* 1    group       Char      1*  |                select                        |  1    group       Char      3* FIXED   */
    /*                                |                  max(length)                 |                                        */
    /*                                |                into                          |                                        */
    /* Data Set Name  WORK.Z2         |                  :lenmax trimmed             |  Data Set Name  WORK.Z2                */
    /* ======================         |                from                          |  =======================               */
    /*  Variables in Creation Order   |                  sashelp.vcolumn             |   Variables in Creation Order          */
    /*                                |                where                         |                                        */
    /* #    Variable    Type    Len   |                       libname="WORK"         |  #    Variable    Type    Len          */
    /*                                |                   and memname eqt "Z"        |                                        */
    /* 1    group       Char      2*  |                   and upcase(name) = "GROUP" |  1    group       Char      3* FIXED   */
    /*                                |             ;quit;                           |                                        */
    /*                                |         '));                                 |                                        */
    /* Data Set Name  WORK.Z3         |       end;                                   |  Data Set Name  WORK.Z3                */
    /* ======================         |                                              |  =======================               */
    /*  Variables in Creation Order   |       max_length = dosubl('                  |   Variables in Creation Order          */
    /*                                |                                              |                                        */
    /* #    Variable    Type    Len   |          data z1 z2 z3;                      |  #    Variable    Type    Len          */
    /*                                |                                              |                                        */
    /* 1    group       Char      3*  |           length group $&lenmax.;            |  1    group       Char      3* FIXED   */
    /*                                |                                              |                                        */
    /*                                |           set z: indsname=zs;                |                                        */
    /*                                |                                              |                                        */
    /*                                |           select (zs);                       |                                        */
    /*                                |             when ("WORK.Z1") output z1;      |                                        */
    /*                                |             when ("WORK.Z2") output z2;      |                                        */
    /*                                |             when ("WORK.Z3") output z3;      |                                        */
    /*                                |           end; /* otherwise not needed */    |                                        */
    /*                                |                                              |                                        */
    /*                                |         run;quit;                            |                                        */
    /*                                |         ');                                  |                                        */
    /*                                |                                              |                                        */
    /*                                |    run;quit;                                 |                                        */
    /*                                |                                              |                                        */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    data z1 (keep=group)
         z2 (keep=group2 rename=group2=group)
         z3 (keep=group3 rename=group3=group);
      group="1";
      group2="12";
      group3="123";
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*       INPUT                                                                                                            */
    /*                                                                                                                        */
    /* Data Set Name  WORK.Z1                                                                                                 */
    /* ======================                                                                                                 */
    /*  Variables in Creation Order                                                                                           */
    /*                                                                                                                        */
    /* #    Variable    Type    Len                                                                                           */
    /*                                                                                                                        */
    /* 1    group       Char      1*                                                                                          */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* Data Set Name  WORK.Z2                                                                                                 */
    /* ======================                                                                                                 */
    /*  Variables in Creation Order                                                                                           */
    /*                                                                                                                        */
    /* #    Variable    Type    Len                                                                                           */
    /*                                                                                                                        */
    /* 1    group       Char      2*                                                                                          */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* Data Set Name  WORK.Z3                                                                                                 */
    /* ======================                                                                                                 */
    /*  Variables in Creation Order                                                                                           */
    /*                                                                                                                        */
    /* #    Variable    Type    Len                                                                                           */
    /*                                                                                                                        */
    /* 1    group       Char      3*                                                                                          */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|
    ;

    data _null_;

      * get meta data about group;
      if _n_=0 then do;
         %let rc=%sysfunc(dosubl('
             proc sql;
                select
                  max(length)
                into
                  :lenmax trimmed
                from
                  sashelp.vcolumn
                where
                       libname="WORK"
                   and memname eqt "Z"
                   and upcase(name) = "GROUP"
             ;quit;
         '));
       end;

       max_length = dosubl('

          data z1 z2 z3;

           length group $&lenmax.;

           set z: indsname=zs;

           select (zs);
             when ("WORK.Z1") output z1;
             when ("WORK.Z2") output z2;
             when ("WORK.Z3") output z3;
           end; /* otherwise not needed */

         run;quit;
         ');

    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*          OUTPUT                                                                                                        */
    /*                                                                                                                        */
    /*   Data Set Name  WORK.Z1                                                                                               */
    /*   ======================                                                                                               */
    /*    Variables in Creation Order                                                                                         */
    /*                                                                                                                        */
    /*   #    Variable    Type    Len                                                                                         */
    /*                                                                                                                        */
    /*   1    group       Char      3* FIXED                                                                                  */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*   Data Set Name  WORK.Z2                                                                                               */
    /*   =======================                                                                                              */
    /*    Variables in Creation Order                                                                                         */
    /*                                                                                                                        */
    /*   #    Variable    Type    Len                                                                                         */
    /*                                                                                                                        */
    /*   1    group       Char      3* FIXED                                                                                  */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*   Data Set Name  WORK.Z3                                                                                               */
    /*   =======================                                                                                              */
    /*    Variables in Creation Order                                                                                         */
    /*                                                                                                                        */
    /*   #    Variable    Type    Len                                                                                         */
    /*                                                                                                                        */
    /*   1    group       Char      3* FIXED                                                                                  */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
