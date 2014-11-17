---
layout: page
title: "Clang UPC Sample Program"
description: ""
---
{% include JB/setup %}

The following simple example is used to demonstrate capabilities
of the Clang UPC toolset.  Copy the lines of code bellow into a
file (e.g. _sample.upc_).

    #include <upc.h>  /* Optional ... */
    #include <stdio.h>
    
    shared int sint[THREADS];
    
    int
    main(void)
    {
      int i;
      for (i=0; i<THREADS; ++i)
        {
          if (i == MYTHREAD)
            {
              sint[MYTHREAD] = MYTHREAD;
              printf ("%d\n", MYTHREAD);
            }
          upc_barrier;
        }
      if (!MYTHREAD)
        {
          for (i=0; i<THREADS; ++i)
            {
              if (sint[i] != i)
                printf ("Error at entry %d (%d)\n", i, sint[i]);
            }
        }
    }
    
And, compile it with the following command:

    clang-upc -o sample sample.upc

Executable, _sample_, is created with the compiler's default options
(packed pointer representation, dynamic number of threads).

Run the executable with five (5) UPC threads:

    ./sample -n 5

and observe the following program output:

<pre>
0
1
2
3
4
</pre>

