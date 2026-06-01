___
```cpp
vctr mtrxMul(const mtrx& m, const vctr& v) // multiply the Weights with the Input
{
int rows = static_cast<int>(m.size());
int cols = static_cast<int>(m[0].size());
vctr result(rows, zero);

for (int i = 0; i < rows; i++){
for (int j = 0; j < cols; j++){
result[i] += m[i][j] * v[j]; // multiply each weight with corresponding input
}
}
return result;
}
```

> **Matrix Multiplication** is an important part of the ANN, where the weights of the Matrix (the columns) are multiplied with the input values. Thus the entire thing is added to `result`. Thus the system uses its weights on the entire dataset. 

- The `rows` of the 2D matrix are the neurons, and the columns of each row are the weights. 