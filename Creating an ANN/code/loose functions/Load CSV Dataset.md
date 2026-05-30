___
In this stage the given CSV file is loaded. It may be the CSV for training, or maybe for testing.

### **Code**

```cpp
bool loadCSV(const string& filename, vector<vctr>& inputs, vector<vctr>& actuals)
{
ifstream file(filename);
if (!file.is_open())
{
cerr << "[ERROR] Could not open: " << filename << "\n";
return false;
}

string line;
int count = 0;

while (getline(file, line)) // basically for each line
{
if (line.empty())
{
continue;
}

stringstream ss(line); // create a stringstream of the line to work on as a file
string value;
  
// First column is the label
getline(ss, value, ','); // Take input as long as u dont get a comma (,)
int label = stoi(value); // Turn the string into a integer

// Remaining 784 columns are pixels
vctr pixels;
pixels.reserve(784); // Already keep 784 spaces ready
while (getline(ss, value, ',')) // basically a for loop
{
pixels.push_back(
stof(value)
/ 255.0F); // Store the value in pixels (Normalized so that values are b/w 0.0 and 1.0)
}

inputs.push_back(std::move(pixels)); // move the entire thing directly instead of copying
actuals.push_back(createOneHotVector(label)); // store the label vector

++count;
if (count % 10000 == 0)
cout << " Loaded " << count << " samples...\n";
}

cout << "Total samples loaded: " << count << "\n";
return true;
}
```

This is a boolean function, meaning it will return true or false, while also editing the given _arguments_:
1. `string& filename`: The name of the CSV file to parse.
2. `vector<vctr>& inputs`: The Input Matrix, with each vector within holding an entire 784 pixels.
3. `vector<vctr>& actuals`: The matrix containing the actual values (labels), each vector being `one_hot` of the label.

>[!NOTE] Note
>See the ampersand `&` in every variable type? It shows that the entire argument given to the function while calling is directly used instead of copying.
>Adding `&` makes it pass the physical location of the arguments

