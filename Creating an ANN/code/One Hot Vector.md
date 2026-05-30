___
### Definition

The One Hot Vector is basically the function through which a single label is turned into a vector, so that it can be compared with the prediction.

###### Code:
```cpp
vctr createOneHotVector(int label, int classes = 10)
{
vctr one_hot(classes, zero);
if (label >= 0 && label < classes)
{
one_hot[label] = 1.0F;
}
return one_hot;
}
```

- `classes` is the number of neurons to alter.
- Each neuron gives a decimal value, which is the probability of the result being that value.
- the `createOneHotVector` turns a integer value (the Label from the first entry of the CSV) into a vector, to be easily compared. (eg. `5` is turned into `[0,0,0,0,0,5,0,0,0,0]` [`one_hot[5] = 5`])