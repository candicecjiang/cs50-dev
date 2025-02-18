# Activity 12 Solutions


1. `v1.c`
The memory allocated in `create_banner` is never freed. Add the statement `free(banner);` after the
`puts(banner);` statement in the `output_report` function.

2. `v2.c`
Just as with 1.: the memory allocated in `create_banner` is never freed. Add the statement
`free(banner);` after the `puts(banner);` statement in the `output_report` function or in the `main`
function just before the `return 0;`.

3. `v3.c`
The memory allocated and stored in the `numbers->nums` is never freed.
Insert the statement `free(numbers->nums);` just before the `return 0;` of the `main` function.

4. `v4.c`
Same problem as in 3: The memory allocated and stored in the `numbers->nums` is never freed.
The statement `numbers = NULL;` loses the pointer to the allocated memory, which prevents ever
being able to free it. Replace that useless statement with:

```c
   // reset numbers - only incremented twice this time 
   numbers -= 2;
 
   free(numbers[0].nums);
   free(numbers[1].nums);
   free(numbers[2].nums);
   free(numbers);
```

5. `v5.c`
The `strcpy` source and destination addresses will overlap if the username is long enough. The result
of such a copy is unpredictable. Fix it by ensuring the `username` field is long enough to hold
the longest possible username, plus the longest possible nickname, plus 1 for the `/` and the trailing NULL.

6. `bagbugs`
Three statements need to be changed.  Here's a diff between the fixed version and the bad original version.

```bash
bagbugs $ diff bagbugsfixed.c tmp/bagbugs/bagbugs.c
62a63
>       bag->head = new;
64d64
<       bag->head = new; // moved after the above statement
98c98
<   } else if (bag->head == NULL) {     // WAS assignment rather than =
---
>   } else if ((bag->head = NULL)) {
104c104
<     mem_free(out);
---
>     mem_free(out->next);
bagbugs $
```

