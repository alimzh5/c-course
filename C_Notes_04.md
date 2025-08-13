### Arrays in C
**1. Basics**
* **Definition**: A collection of elements of the same type stored in sequential memory locations.

* **Common uses**:

  * Normal data storage

  * Buffers

  * Strings

**2. Buffer usage**
* **Case 1 – Temporary read/write storage:**
Used when you need a place to store data before processing (e.g., reading from a file, writing to a device).

* **Case 2 – Input aggregation:**
When multiple inputs arrive at once, the system stores them in a buffer before sending them to slower storage (like a hard drive) to avoid performance issues and reduce wear.

* Memory layout example:

```
[   buffer   ][permissions]
```
**3. Examples**
```
int A;              // single integer
int B[10];          // array of 10 integers
char c[40];         // array of 40 characters

int D[5] = {1,2,3,4,5};  // fully initialized
int E[5] = {1,2,3};      // partially initialized, rest = 0
int F[] = {1,2,3};       // size inferred as 3

int x = 6;
int G[x];           // variable-length array (VLA, size fixed after declaration)
```
**Note**: You cannot resize an array in C after creation.

**4. Multidimensional arrays**
```
int H[2][3];  // 2 rows × 3 columns = 6 elements
H[1][2];      // element at row 1, column 2 → index = 1*3 + 2 = 5

int I[2][3][4]; // 3D array: 2 × 3 × 4 = 24 elements
```
* Memory is stored in row-major order (last index changes fastest).

*******

![Alt Text](https://github.com/alimzh5/c-course/blob/main/repository/ARRAY.png)
******

### Pointer Arithmetic Example
In C, the name of an array (e.g., `A`) represents the address of its first element.

* `A` → address of the first element (`&A[0]`)

* `A + 2` → address of the third element (`&A[2]`)

Example:

```
int test = 0;
printf("%ld\n", A + 2);  // prints address of A[2]
printf("%ld\n", &test);  // prints address of variable test
```
Pointer arithmetic automatically accounts for the size of the data type. For example, with `int` (usually 4 bytes), `A + 2` moves 8 bytes ahead from `A`.

*******

In C, when you write `A` for an array, it represents the address of the first element. Writing `A + 2` moves the pointer by 2 elements, not 2 bytes. The actual memory offset depends on the data type size (e.g., for `int`, it moves `2 * sizeof(int)` bytes). Using `*(A + 2)` accesses the value at the third element of the array.

```
*(A + 2)

```
****
