___
> [!NOTE] Note:
> **ReLU** stands for _Rectified Linear Unit_.
> Here, we have applied Leaky ReLU at the function to predict, and this function is just for its derivation
> You can see Prediction for the applying of ReLU

```cpp
vctr reluDeriv(const vctr& z)
{
vctr d(z.size(), zero);

for (size_t i = 0; i < z.size(); i++)
{d[i] = (z[i] > 0.0F) ? 1.0F : 0.01F;} // derivation of the relu neurons;

return d;
}
```



