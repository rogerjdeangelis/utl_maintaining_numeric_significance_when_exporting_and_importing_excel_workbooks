# utl_maintaining_numeric_significance_when_exporting_and_importing_excel_workbooks
Maintaining numeric significance when exporting and importing excel workbooks. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverfl SAS community.
    Maintaining numeric significance when exporting and importing excel workbooks

    see github
    https://goo.gl/ExG9V6
    https://github.com/rogerjdeangelis/utl_maintaining_numeric_significance_when_exporting_and_importing_excel_workbooks

     Same result WPS/SAS

        WPS supports the excel engine in base/wps

    Original Topic: How to import from xls to sas dataset and keep all figures after 'dot'

    I don't use 'proc import/export', my hope is that SAS will deprecate this functionality
    since there are beter ways to deal with excel ie SA/WPS/ engines or R.
    A big advantage of 'libname engines' is that you do not have to create a SAS/WPS dataset.
    Obviously you can easily create one if you want.

    Libanme excel does not exhibit the issue, not sure about 'proc import/export'.

    see
    https://goo.gl/K6uFJE
    https://communities.sas.com/t5/Base-SAS-Programming/How-to-import-from-xls-to-sas-dataset-and-keep-all-figures-after/m-p/434155



    INPUT (XLS sheet)
    =================

       If exported with the SAS/WPS libname egines (did not check 'proc import/export')
       Althoug excel only shows 8 significant digits the underlying data is IEEE 754 double floats

       d:/xls/utl_maintaining_numeric_significance_when_exporting_and_importing_excel_workbooks.xlsx

          +--------------------------------------+
          |     A      |    B       |     C      |
          +--------------------------------------+
       1  |   PI       |   EULER    |            |
          +------------+------------+------------+
       2  |0.031415927 |            |            |
          +------------+------------+------------+
       3  |0.031415927 | 0.00577215 |            |
          +------------+------------+------------+
       20 | WILLIAM    |    M       |            |
          +------------+------------+------------+



    PROCESS (all the code)
    ======================

    * read the excel sheet that visually shows rounded results;

    libname xel "d:/xls/utl_maintaining_numeric_significance_when_exporting_and_importing_excel_workbooks.xlsx";
    proc print data=xel.result;
      title "libname engine maintains all significant digits";
      format pi euler 20.17;
    run;quit;



    OUTPUT
    ======

      libname engine maintains all significant digits

                         PI                   EULER

        0.03141592653589790      .
        0.03141592653589790     0.00577215664901533

    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

    libname xel "d:/xls/utl_maintaining_numeric_significance_when_exporting_and_importing_excel_workbooks.xlsx";
    data chkResult;
       set xel.result;
       put pi 20.17;
        put euler 20.17;
    run;quit;
    libname xel clear;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    %utl_submit_wps64('
    libname xel excel "d:/xls/utl_maintaining_numeric_significance_when_exporting_and_importing_excel_workbooks.xlsx";
    proc print data=xel.result;
      title "libname engine maintains all significant digits";
      format pi euler 20.17;
    run;quit;
    libname xel clear;
    ');

    *                      __                   _       _                 _
    __      ___ __  ___   / /__  __ _ ___    __| | __ _| |_ __ _ ___  ___| |_
    \ \ /\ / / '_ \/ __| / / __|/ _` / __|  / _` |/ _` | __/ _` / __|/ _ \ __|
     \ V  V /| |_) \__ \/ /\__ \ (_| \__ \ | (_| | (_| | || (_| \__ \  __/ |_
      \_/\_/ | .__/|___/_/ |___/\__,_|___/  \__,_|\__,_|\__\__,_|___/\___|\__|
             |_|
    ;

    libname xel "d:/xls/utl_maintaining_numeric_significance_when_exporting_and_importing_excel_workbooks.xlsx";
    data chkResult;
       set xel.result;
       put pi 20.17;
        put euler 20.17;
    run;quit;
    libanme xel clear;

