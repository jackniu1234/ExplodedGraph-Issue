# ExplodedGraph-Issue
I' m now trying to understand the ExplodedGraph of clang static analyzer using debug.ViewExplodedGraph checker and I hope to select some ExplodedNode to achieve the effect of function summary. However, I found CSA sometimes throws constraints in the subsequent ExplodedNode on a branch, which makes it impossible to just use one ExplodedNode without considering the previous nodes.

Here are two simple examples with similar code. The example 1 throwed constraints while example 2 didn't.

Code of example 1:
```c
#include <stdio.h>

int main() {
    int a;
    scanf("%d", &a);

    if (a > 10) {
        a = a + 1;
    }
    else {
        a = a + 2;
    }
    return a;
}
```
The ExplodedGraph like this:
![](./right.png)

Here are two simple examples with similar code. The example 1 throwed constraints while example 2 didn't.

Code of example 1:
```c
int rand();
int main() {
    int a = 2;

    if (rand() > 10) {
        a = a + 1;
    }
    else {
        a = a+ 2;
    }
    return 0;
}
```

The ExplodedGraph like this:
![](./wrong.png)