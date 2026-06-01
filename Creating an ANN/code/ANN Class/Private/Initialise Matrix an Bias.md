___
```cpp
mtrx initMatrix(int rows, int cols)
{
mtrx m(rows, vctr(cols, zero)); // create a matrix
mt19937 gen(42); // random numbers generation
uniform_real_distribution<float> dis(-0.1F, 0.1F); // distribution chart b/w -0.1 and 0.1
 
for (auto& row : m){
for (auto& val : row){
val = dis(gen);
}
}
return m;
}
```

#### **Concept**:
- This is a `matrix` type function (`mtrx` type is a shorthand of `vector<vector<float>>`). It will return a `matrix ` type only.
- `mtrx m(rows, vctr(cols, zero))` creates the matrix with `rows` number of rows and each row contains a vector with `cols` number of values each equal to 0.0F .
- `mt19937 gen(42)` creates an object of random numbers and saves it to `gen` name. `mt19937` is Mersenne Twister algorithm from the `random` header. The seed `42` always gives the same output.
- `uniform_real_distribution<float> dis(-0.1F, 0.1F)` creates a uniform distribution chart, where values are between -0.1 and 0.1 . 
- In the 2 for loops, for each row in matrix m, and each value in the rows, the value is written as the random gen, passed through the distribution chart.
- After the code is run, the new matrix m is returned. 
- This is done so that for future use in other datasets, the code can easily be tweaked instead of a full rewrite.

#### **Bias vector Initialisation**: 
(same as the matrix)

```cpp
vctr initVector(int size) // same as initmatrix but for the bias vector
{
vctr v(size, zero);
mt19937 gen(42);
uniform_real_distribution<float> dis(-0.1F, 0.1F);

for (auto& val : v){
val = dis(gen);
}

return v;
}
```

_Since this follows the precisely same logic as the initMatrix, I didn't again write it._ 