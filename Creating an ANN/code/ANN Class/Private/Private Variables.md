___
```cpp
private: // Only the ai can touch its brain

mtrx mat; // The 2D vector matrix
vctr bias; // the bias vector
vctr last_z; // The last pre-activation values
float learning_rate;
```

#### **Logic**:
- The variables such as the neuron matrix (`mat`), the `bias` vector, the last copy of the pre-activation values and `learning_rate` are kept in the private part of the class.
- The class is used as C++ is an OOP language.