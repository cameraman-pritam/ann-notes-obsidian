***
An ANN works extensively on Higher Mathematics, namely Calculus, and Linear Calculations.

The Maths Behind ANNs can be found in detail [[Maths Behind ANNs|Here]].

In CPP, an ANN is completely kept within a `std::vector` . A Vector is used because in C++, it stores values in RAM, and not SSD, meaning faster overall time and speed. Also, to save the model, the matrix(A two dimensional vector `std::vector<std::vector<float>>` and the vector can easily be turned into a binary file, for fast retrieval of data. After the code runs completely, the entire training is lost otherwise, as all the biases, weights, etc. are cleaned from RAM. 

After the ANN has been created, it is compiled with `clang++`, if it has no _conan_ dependencies. Otherwise `cmake` is used. Also, to interface it with a frontend stack (eg. _ReactJS_), the code it compiled into _WebAssembly_ (or `wasm` ) using `EmScripten`  (see [here](https://emscripten.org/) ).

*** 
## Starting of the Code

Before the code starts, lets look at the basic things:
###### **Libraries Used** :
```cpp
#include <algorithm>
#include <fstream>
#include <ios>
#include <iostream>
#include <numeric>
#include <random>
#include <sstream>
#include <string>
#include <vector>
using namespace std;
```

- `algorithm`: a powerful collection of built-in functions designed to perform common operations like sorting, searching, counting, and manipulating data structures.
- `fstream`: File Stream for file I/O.
- `ios`: Basic I/O formatting
- `iostream`: _Well, does this one need to be written?_
- `vector`: To conduct operations on `std::vector`.
- `string`: To conduct operations on `std::string`.
- `sstream`: [_String Stream_] To do `fstream` like operations on strings.
- `random`: a robust and statistically sound framework used to generate pseudo-random numbers.

> [!NOTE] **Note**
> While in my code I have included `namespace std`, it is a good practice not to do so. For smaller projects this doesn't affect anything, but in higher sized projects, it can slow down the entire code compilation, as entire of the `std` namespace is imported regardless of use. _I am just too lazy.._, so I just include it anyway..

###### **Shorthand Syntaxes**:
To have something short to type instead of typing `std::vector<float>`, or `std::vector<std::vector<float>>`, so these are what I use:

```cpp
using vctr = vector<float>;
using mtrx = vector<vctr>; //basically vector<vector<float>>
constexpr float zero = 0.0F;
```

- `vctr`: can be used as `vctr bias` instead of `vector<float> bias`.
- `mtrx`: can be easily used as `mtrx matr` as `vector<vector<float>> matr`.
- `constexpr zero`: shorthand for `0.0F` (_0, but only upto float_).

>[!NOTE] **Note**
>See the use of `vector<>` instead of `std::vector<>`?  That's because I have already imported `namespace std`!

***
### The Code Itself

> [!NOTE] Note
>  1. This All code that you see here is for an example code which uses [MNIST](https://en.wikipedia.org/wiki/MNIST_database) Dataset, which is for Handwritten Numbers. It is available as CSV download on [Kaggle](https://www.kaggle.com/datasets/hojjatk/mnist-dataset).
> 2. This dataset contains 10 types of results `[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]` and thus there are 10 neurons in this example.
> 3. Each image of a handwritten number is turned into a set of 784 floats (for each image is 28x28 pixels) each from value 0 to 255.
> 4. Each line contains 786 values, the first one is the actual value (0-9) and the next 784 values of pixels, comma separated.

- **See _Loose Functions_** [[Loose Functions|Here]].