# utl-select-distinct-values-of-one-variables-grouped-by-another-variable-in-wps-r-and-python
Select distinct values of one variables grouped by another variable in wps r and python
    %let pgm=utl-select-distinct-values-of-one-variables-grouped-by-another-variable-in-wps-r-and-python;

    Select distinct values of one variables grouped by another variable in wps r and python

    SOLUTIONS

        1 wps sql
        2 wps r
        3 wps python
        4 wps r no sql

    github
    https://tinyurl.com/28wzar6m
    https://github.com/rogerjdeangelis/utl-select-distinct-values-of-one-variables-grouped-by-another-variable-in-wps-r-and-python

    Stackoverflow R
    https://tinyurl.com/bdz4jnvv
    https://stackoverflow.com/questions/77565913/show-value-in-one-variable-for-distinct-values-in-another-variable-in-r

    /**************************************************************************************************************************/
    /*                               |                                                                                        */
    /*                               |                                                                                        */
    /*                               |                                                                                        */
    /*          INPUT                |       OUTPUT                                                                           */
    /*                               |                                                                                        */
    /*                               | GROUP BY  DISTINCT                                                                     */
    /*  Obs    CYL    GEAR     HP    |   CYL       GEAR                                                                       */
    /*                               |                                                                                        */
    /*    1     4       3      97    |    4          3                                                                        */
    /*    2     4       4      93    |    4          4                                                                        */
    /*    3     4       4      62    |    4          5                                                                        */
    /*    4     4       4      95    |                                                                                        */
    /*    5     4       4      66 =  |                                                                                        */
    /*    6     4       4      66 =  |                                                                                        */
    /*    7     4       4      65    |                                                                                        */
    /*    8     4       4      52    |                                                                                        */
    /*    9     4       4     109    |                                                                                        */
    /*   10     4       5      91    |                                                                                        */
    /*   11     4       5     113    |                                                                                        */
    /*                               |                                                                                        */
    /*   12     6       3     105    |    6          3                                                                        */
    /*   13     6       3     110 =  |    6          4                                                                        */
    /*   14     6       4     110 =  |    6          5                                                                        */
    /*   15     6       4     110 =  |                                                                                        */
    /*   16     6       4     123 =  |                                                                                        */
    /*   17     6       4     123 =  |                                                                                        */
    /*   18     6       5     175    |                                                                                        */
    /*                               |                                                                                        */
    /*   19     8       3     245 =  |    8          3                                                                        */
    /*   20     8       3     245 =  |    8          5                                                                        */
    /*   21     8       3     180 =  |                                                                                        */
    /*   22     8       3     180 =  |                                                                                        */
    /*   23     8       3     180 =  |                                                                                        */
    /*   24     8       3     205    |                                                                                        */
    /*   25     8       3     215    |                                                                                        */
    /*   26     8       3     230    |                                                                                        */
    /*   27     8       3     150 =  |                                                                                        */
    /*   28     8       3     150 =  |                                                                                        */
    /*   29     8       3     175 =  |                                                                                        */
    /*   30     8       3     175 =  |                                                                                        */
    /*   31     8       5     264    |                                                                                        */
    /*   32     8       5     335    |                                                                                        */
    /*                               |                                                                                        */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
    input cyl gear hp ;
    cards4;
    4 3 97
    4 4 93
    4 4 62
    4 4 95
    4 4 66
    4 4 52
    4 4 65
    4 4 66
    4 4 109
    4 5 91
    4 5 113
    6 3 110
    6 3 105
    6 4 110
    6 4 110
    6 4 123
    6 4 123
    6 5 175
    8 3 175
    8 3 245
    8 3 180
    8 3 180
    8 3 180
    8 3 205
    8 3 215
    8 3 230
    8 3 150
    8 3 150
    8 3 245
    8 3 175
    8 5 264
    8 5 335
    ;;;;
    run;quit;

    /*                                  _
    / | __      ___ __  ___   ___  __ _| |
    | | \ \ /\ / / `_ \/ __| / __|/ _` | |
    | |  \ V  V /| |_) \__ \ \__ \ (_| | |
    |_|   \_/\_/ | .__/|___/ |___/\__, |_|
                 |_|                 |_|
    */

    proc datasets lib=sd1 nolist nodetails;delete want; run;quit;

    %utl_submit_wps64x('
    libname sd1 "d:/sd1";
    proc sql;
      create
         table sd1.want as
      select
         distinct cyl, gear
      from
         sd1.have
    ;quit;
    ');

    proc print data=sd1.want width=min;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  SD1.WANT total obs=8                                                                                                  */
    /*                                                                                                                        */
    /*  Obs    CYL    GEAR                                                                                                    */
    /*                                                                                                                        */
    /*   1      4       3                                                                                                     */
    /*   2      4       4                                                                                                     */
    /*   3      4       5                                                                                                     */
    /*   4      6       3                                                                                                     */
    /*   5      6       4                                                                                                     */
    /*   6      6       5                                                                                                     */
    /*   7      8       3                                                                                                     */
    /*   8      8       5                                                                                                     */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___                                          _
    |___ \  __      ___ __  ___   _ __   ___  __ _| |
      __) | \ \ /\ / / `_ \/ __| | `__| / __|/ _` | |
     / __/   \ V  V /| |_) \__ \ | |    \__ \ (_| | |
    |_____|   \_/\_/ | .__/|___/ |_|    |___/\__, |_|
                     |_|                        |_|
    */

    proc datasets lib=sd1 nolist nodetails;delete want; run;quit;

    %utl_submit_wps64x('
    libname sd1 "d:/sd1";
    proc r;
    export data=sd1.have r=have;
    submit;
    library(sqldf);
    want=sqldf("
      select
         distinct cyl, gear
      from
         have
    ");
    want;
    endsubmit;
    import data=sd1.want r=want;
    run;quit;
    proc print data=sd1.want width=min;
    run;quit;
    ');

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  The WPS R System       The WPS System                                                                                 */
    /*                                                                                                                        */
    /*    CYL GEAR          Obs    CYL    GEAR                                                                                */
    /*                                                                                                                        */
    /*  1   6    4           1      6       4                                                                                 */
    /*  2   4    4           2      4       4                                                                                 */
    /*  3   6    3           3      6       3                                                                                 */
    /*  4   8    3           4      8       3                                                                                 */
    /*  5   4    3           5      4       3                                                                                 */
    /*  6   4    5           6      4       5                                                                                 */
    /*  7   8    5           7      8       5                                                                                 */
    /*  8   6    5           8      6       5                                                                                 */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____                                  _
    |___ /  __      ___ __  ___   ___  __ _| |  _ __  _   _
      |_ \  \ \ /\ / / `_ \/ __| / __|/ _` | | | `_ \| | | |
     ___) |  \ V  V /| |_) \__ \ \__ \ (_| | | | |_) | |_| |
    |____/    \_/\_/ | .__/|___/ |___/\__, |_| | .__/ \__, |
                     |_|                 |_|   |_|    |___/
    */

    proc print data=sd1.want width=min;
    run;quit;

    proc datasets lib=sd1 nolist nodetails;delete want; run;quit;

    %utl_submit_wps64x("
    options validvarname=any lrecl=32756;
    libname sd1 'd:/sd1';
    proc python;
    export data=sd1.have python=have;
    submit;
    import pyreadstat;
    from os import path;
    import pandas as pd;
    import numpy as np;
    from pandasql import sqldf;
    mysql = lambda q: sqldf(q, globals());
    from pandasql import PandaSQL;
    pdsql = PandaSQL(persist=True);
    sqlite3conn = next(pdsql.conn.gen).connection.connection;
    sqlite3conn.enable_load_extension(True);
    sqlite3conn.load_extension('c:/temp/libsqlitefunctions.dll');
    mysql = lambda q: sqldf(q, globals());
    want = pdsql('''
      select
         distinct cyl, gear
      from
         have

    ''');
    print(want);
    pyreadstat.write_xport(want, 'd:/xpt/want.xpt',table_name='want',file_format_version=5);
    endsubmit;
    run;quit;
    ");

    libname xpt xport "d:/xpt/want.xpt";
    proc contents data=xpt._all_;
    run;quit;
    data want;
      set xpt.want;
    run;quit;
    proc print;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* The WPS PYTHON Procedure      The WPS System                                                                           */
    /*                                                                                                                        */
    /*     CYL  GEAR               Obs    CYL    GEAR                                                                         */
    /*                                                                                                                        */
    /*  0  6.0   4.0                1      6       4                                                                          */
    /*  1  4.0   4.0                2      4       4                                                                          */
    /*  2  6.0   3.0                3      6       3                                                                          */
    /*  3  8.0   3.0                4      8       3                                                                          */
    /*  4  4.0   3.0                5      4       3                                                                          */
    /*  5  4.0   5.0                6      4       5                                                                          */
    /*  6  8.0   5.0                7      8       5                                                                          */
    /*  7  6.0   5.0                8      6       5                                                                          */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*  _                                                  _
    | || |   __      ___ __  ___   _ __   ___    ___  __ _| |
    | || |_  \ \ /\ / / `_ \/ __| | `_ \ / _ \  / __|/ _` | |
    |__   _|  \ V  V /| |_) \__ \ | | | | (_) | \__ \ (_| | |
       |_|     \_/\_/ | .__/|___/ |_| |_|\___/  |___/\__, |_|
                      |_|                               |_|
    */

    %utl_submit_wps64x('
    libname sd1 "d:/sd1";
    proc r;
    export data=sd1.have r=have;
    submit;
    have;
    library(dplyr);
    want<-have[,c("CYL","GEAR")] %>%
      group_by(CYL) %>%
      summarise(GEAR=unique(GEAR));
    want;
    endsubmit;
    import data=sd1.want r=want;
    run;quit;
    proc print data=sd1.want width=min;
    run;quit;
    ');


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*     WPS  R                       WPS                                                                                   */
    /*                                                                                                                        */
    /*  # A tibble: 8 x 2                                                                                                     */
    /*  # Groups:   CYL [3]                                                                                                   */
    /*      CYL  GEAR            Obs    CYL    GEAR                                                                           */
    /*    <dbl> <dbl>                                                                                                         */
    /*  1     4     4             1      4       4                                                                            */
    /*  2     4     3             2      4       3                                                                            */
    /*  3     4     5             3      4       5                                                                            */
    /*  4     6     4             4      6       4                                                                            */
    /*  5     6     3             5      6       3                                                                            */
    /*  6     6     5             6      6       5                                                                            */
    /*  7     8     3             7      8       3                                                                            */
    /*  8     8     5             8      8       5                                                                            */
    /*                                                                                                                        */
    /**************************************************************************************************************************/


    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */


























































Transposing words into sentences using sql partitioning in r and python

I know, wps proc transpose, can easily solve this problem, but I want to show R and Python sql solutions.

github
https://tinyurl.com/444nvehx
https://github.com/rogerjdeangelis/utl-transposing-words-into-sentences-using-sql-partitioning-in-r-and-python

stackoverflow R
https://tinyurl.com/bdh5tah5
https://stackoverflow.com/questions/77571002/how-to-retrieve-all-texts-that-a-word-appear

None of the posted R solutions create a dataframe.

1. r hardcode sql
2. r dynamic sql
3. related repos
4. all r solution
5. same code will work in python pandasql (see repos on end)

SOAPBOX ON

  Although the R solutions are simple, none of th solutions result in a dataframe.
  I consider this a flaw in R solutions because converting datastructures to
  dataframes can be very challenging. SQL guanrantees a dataframe and
  the code is universal. Python is even more troublesome.

  Converting the R output list datastructures to a dataframe can take more code
  then some of the R solutions.

SOAPBOX OFF


github Macro to enable partitioning in wps proc sql.
https://tinyurl.com/3c3vzps5
https://github.com/rogerjdeangelis/utl-macro-to-enable-sql-partitioning-by-groups-montonic-first-and-last-dot

/*                   _
(_)_ __  _ __  _   _| |_
| | `_ \| `_ \| | | | __|
| | | | | |_) | |_| | |_
|_|_| |_| .__/ \__,_|\__|
        |_|
*/

options validvarname=upcase;
libname sd1 "d:/sd1";
data sd1.have;
 input word $1. text;
cards4;
a 1
a 2
a 5
b 1
b 3
c 1
c 3
c 4
d 4
e 2
e 4
f 3
g 2
h 5
i 5
;;;;
run;quit;

/*            _                   _               _          _             _
/ |    _ __  | |__   __ _ _ __ __| | ___ ___   __| | ___  __| |  ___  __ _| |
| |   | `__| | `_ \ / _` | `__/ _` |/ __/ _ \ / _` |/ _ \/ _` | / __|/ _` | |
| |_  | |    | | | | (_| | | | (_| | (_| (_) | (_| |  __/ (_| | \__ \ (_| | |
|_(_) |_|    |_| |_|\__,_|_|  \__,_|\___\___/ \__,_|\___|\__,_| |___/\__, |_|
                                                                        |_|
*/

proc datasets lib=sd1 nolist nodetails;delete want; run;quit;

%utl_submit_wps64x("
libname sd1 'd:/sd1';
proc r;
export data=sd1.have r=have;
submit;
library(sqldf);
want<-sqldf('
   select
      word
     ,max(case when partition=1 then text else NULL end) as text1
     ,max(case when partition=2 then text else NULL end) as text2
     ,max(case when partition=3 then text else NULL end) as text3
   from
     ( select word, text, row_number() OVER (PARTITION BY word) as partition from have )
   group
     by word;
   ');
want;
endsubmit;
import data=sd1.want r=want;
run;quit;
");

proc print data=sd1.want;
run;quit;

/**************************************************************************************************************************/
/*                                                                                                                        */
/* SD1.WANT total obs=9                                                                                                   */
/*                                                                                                                        */
/*  WORD    TEXT1    TEXT2    TEXT3                                                                                       */
/*                                                                                                                        */
/*   a        1        2        5                                                                                         */
/*   b        1        3        .                                                                                         */
/*   c        1        3        4                                                                                         */
/*   d        4        .        .                                                                                         */
/*   e        2        4        .                                                                                         */
/*   f        3        .        .                                                                                         */
/*   g        2        .        .                                                                                         */
/*   h        5        .        .                                                                                         */
/*   i        5        .        .                                                                                         */
/*                                                                                                                        */
/**************************************************************************************************************************/


/*___               _                             _                  _
|___ \   _ __    __| |_   _ _ __   __ _ _ __ ___ (_) ___   ___  __ _| |
  __) | | `__|  / _` | | | | `_ \ / _` | `_ ` _ \| |/ __| / __|/ _` | |
 / __/  | |    | (_| | |_| | | | | (_| | | | | | | | (__  \__ \ (_| | |
|_____| |_|     \__,_|\__, |_| |_|\__,_|_| |_| |_|_|\___| |___/\__, |_|
                      |___/                                       |_|
*/

%let maxWords=3;

%array(_wd,values=1-&maxWords);

proc datasets lib=sd1 nolist nodetails;delete want; run;quit;

%utl_submit_wps64x("
libname sd1 'd:/sd1';
proc r;
export data=sd1.have r=have;
submit;
library(sqldf);
want<-sqldf('
   select
      word
     ,%do_over(_wd,phrase=%str(
         max(case when partition=? then text else NULL end) as text?),between=comma)
   from
     ( select word, text, row_number() OVER (PARTITION BY word) as partition from have )
   group
     by word;
   ');
want;
endsubmit;
import data=sd1.want r=want;
run;quit;
");

proc print data=sd1.want;
run;quit;

/**************************************************************************************************************************/
/*                                                                                                                        */
/* SD1.WANT total obs=9                                                                                                   */
/*                                                                                                                        */
/*  WORD    TEXT1    TEXT2    TEXT3                                                                                       */
/*                                                                                                                        */
/*   a        1        2        5                                                                                         */
/*   b        1        3        .                                                                                         */
/*   c        1        3        4                                                                                         */
/*   d        4        .        .                                                                                         */
/*   e        2        4        .                                                                                         */
/*   f        3        .        .                                                                                         */
/*   g        2        .        .                                                                                         */
/*   h        5        .        .                                                                                         */
/*   i        5        .        .                                                                                         */
/*                                                                                                                        */
/**************************************************************************************************************************/

/*
 _ __ ___ _ __   ___  ___
| `__/ _ \ `_ \ / _ \/ __|
| | |  __/ |_) | (_) \__ \
|_|  \___| .__/ \___/|___/
         |_|
*/

REPO
----------------------------------------------------------------------------------------------------------------------------------
https://github.com/rogerjdeangelis/utl-find-first-n-observations-per-category-using-proc-sql-partitioning
https://github.com/rogerjdeangelis/utl-macro-to-enable-sql-partitioning-by-groups-montonic-first-and-last-dot
https://github.com/rogerjdeangelis/utl-transpose-pivot-wide-using-sql-partitioning-in-wps-r-python
https://github.com/rogerjdeangelis/utl-transposing-rows-to-columns-using-proc-sql-partitioning
https://github.com/rogerjdeangelis/utl-using-sql-in-wps-r-python-select-the-four-youngest-male-and-female-students-partitioning


/*                _       _   _
 _ __   ___  ___ | |_   _| |_(_) ___  _ __  ___
| `__| / __|/ _ \| | | | | __| |/ _ \| `_ \/ __|
| |    \__ \ (_) | | |_| | |_| | (_) | | | \__ \
|_|    |___/\___/|_|\__,_|\__|_|\___/|_| |_|___/

*/


/*---- runs all the R solutions                                          ----*/


%utl_submit_wps64x('
libname sd1 "d:/sd1";
proc r;
export data=sd1.have r=have;
submit;
library(tidyverse);
want<-split(have$TEXT, have$WORD);
str(want);
txx<-unstack(have, TEXT~WORD);
str(txx);
xx<-map(unique(have$WORD),\(x){
        have %>% filter(WORD==x) %>% pull(TEXT)
  }) %>%
  purrr::set_names(unique(have$WORD));
str(xx);
endsubmit;
');

They all output lists

The WPS System

List of 9
 $ a: num [1:3] 1 2 5
 $ b: num [1:2] 1 3
 $ c: num [1:3] 1 3 4
 $ d: num 4
 $ e: num [1:2] 2 4
 $ f: num 3
 $ g: num 2
 $ h: num 5
 $ i: num 5

List of 9
 $ a: num [1:3] 1 2 5
 $ b: num [1:2] 1 3
 $ c: num [1:3] 1 3 4
 $ d: num 4
 $ e: num [1:2] 2 4
 $ f: num 3
 $ g: num 2
 $ h: num 5
 $ i: num 5

List of 9
 $ a: num [1:3] 1 2 5
 $ b: num [1:2] 1 3
 $ c: num [1:3] 1 3 4
 $ d: num 4
 $ e: num [1:2] 2 4
 $ f: num 3
 $ g: num 2
 $ h: num 5
 $ i: num 5


/*              _
  ___ _ __   __| |
 / _ \ `_ \ / _` |
|  __/ | | | (_| |
 \___|_| |_|\__,_|

*/







%utl_submit_wps64x("
  proc r;
  submit;
  library(dplyr);
  mtcars;
  mtcars[,c('hp','cyl','gear')] %>%
  group_by(cyl) %>%
  summarise(gear=unique(gear));
  endsubmit;
");



  mtcars[,c('hp','cyl','gear')] %>%
  group_by(cyl) %>%
  summarise(gear=unique(gear));



                   cyl   hp gear
Mazda RX4            6  110    4
Mazda RX4 Wag        6  110    4
Datsun 710           4   93    4
Hornet 4 Drive       6  110    3
Hornet Sportabout    8  175    3
Valiant              6  105    3
Duster 360           8  245    3
Merc 240D            4   62    4
Merc 230             4   95    4
Merc 280             6  123    4
Merc 280C            6  123    4
Merc 450SE           8  180    3
Merc 450SL           8  180    3
Merc 450SLC          8  180    3
Cadillac Fleetwood   8  205    3
Lincoln Continental  8  215    3
Chrysler Imperial    8  230    3
Fiat 128             4   66    4
Honda Civic          4   52    4
Toyota Corolla       4   65    4
Toyota Corona        4   97    3
Dodge Challenger     8  150    3
AMC Javelin          8  150    3
Camaro Z28           8  245    3
Pontiac Firebird     8  175    3
Fiat X1-9            4   66    4
Porsche 914-2        4   91    5
Lotus Europa         4  113    5
Ford Pantera L       8  264    5
Ferrari Dino         6  175    5
Maserati Bora        8  335    5
Volvo 142E           4  109    4


data have;
input cyl gear hp ;
cards4;
6  4  110
6  4  110
4  4   93
6  3  110
8  3  175
6  3  105
8  3  245
4  4   62
4  4   95
6  4  123
6  4  123
8  3  180
8  3  180
8  3  180
8  3  205
8  3  215
8  3  230
4  4   66
4  4   52
4  4   65
4  3   97
8  3  150
8  3  150
8  3  245
8  3  175
4  4   66
4  5   91
4  5  113
8  5  264
6  5  175
8  5  335
4  4  109
;;;;
run;quit;

/**************************************************************************************************************************/
/*                                                                                                                        */
/*     WPS  R                       WPS                                                                                   */
/*                                                                                                                        */
/*  # A tibble: 8 x 2                                                                                                     */
/*  # Groups:   CYL [3]                                                                                                   */
/*      CYL  GEAR            Obs    CYL    GEAR                                                                           */
/*    <dbl> <dbl>                                                                                                         */
/*  1     4     4             1      4       4                                                                            */
/*  2     4     3             2      4       3                                                                            */
/*  3     4     5             3      4       5                                                                            */
/*  4     6     4             4      6       4                                                                            */
/*  5     6     3             5      6       3                                                                            */
/*  6     6     5             6      6       5                                                                            */
/*  7     8     3             7      8       3                                                                            */
/*  8     8     5             8      8       5                                                                            */
/*                                                                                                                        */
/**************************************************************************************************************************/
