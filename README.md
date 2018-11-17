# utl-evaluate-recursive-ackermann-function-in-SAS-and-Python
Evaluate recursive Ackermann function.
    Evaluate recursive Ackermann function

       Two Solutions

            1. Python
            2. SAS macro (I think there may be a DOSUBL solution but we need a smart compiler)


    https://tinyurl.com/yca4gbgm
    https://github.com/rogerjdeangelis/utl-evaluate-recursive-ackermann-function-in-SAS-and-Python

    macros
    https://tinyurl.com/y9nfugth
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories

    https://tinyurl.com/y95k5bsd
    https://stackoverflow.com/questions/53351519/writing-the-ackermann-function-in-a-sas-data-step

    SAS Macro
    https://stackoverflow.com/users/4965549/tom

    Python code
    http://pythonfiddle.com/ackermanns-function/


    INPUT
    =====

      M=2
      N=3


    EXAMPLE OUTPUT (same for SAS and Python)
    ----------------------------------------

    9

    Note the Ackermann function blows up for small values on m and n


    PROCESS
    =======

    1. Python  (output in output window)
    ------------------------------------

    %utl_submit_py64("
    import sys;
    sys.setrecursionlimit(30000);
    memo = {};
    def ack(m, n):;
    .   if not (m, n) in memo:;
    .       result = (n + 1) if m == 0 else (;
    .           ack(m-1, 1) if n == 0 else ack(m-1, ack(m, n-1)));
    .       memo[(m, n)] = result;
    .   return memo[(m, n)];
    print ack(2, 3);
    ");

    2. SAS macro
    ------------
    %utlnopts;
    %macro ack(m,n);
    %if (&m=0) %then %eval(&n+1);
    %else %if (&n=0) %then %ack(%eval(&m-1),1);
    %else %ack(%eval(&m-1),%ack(&m,%eval(&n-1)));
    %mend ack;

    %put %ack(2,3);


