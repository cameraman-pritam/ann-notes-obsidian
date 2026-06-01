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

#### **Bit by bit explanation**

```cpp
ifstream file(filename);
if (!file.is_open())
{
cerr << "[ERROR] Could not open: " << filename << "\n";
return false;
}
```

1. create a input file stream of `filename` named `file`.
2. check if file is _not_ accessible (`if (!file.is_open())`) and if file is not accessible, return false and stop. 

```cpp
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
```

1. `while` loop recursively checks for each line in the file, and saves it in a string.
2. `if` any line is blank, skip.
3. `streangstream` turn line string into a `stringstream` called `ss`, which can be processed like an ordinary file.
4. `getline` parses `ss` as an ordinary file, reads upto the first comma, stores the string in `value`. The label `value` is assigned to an integer variable.
5. `pixels.reserve(784)` tells the machine to already keep 784 reserved spaces in the RAM. Thus, the entire image binary can be easily moved instead of running time for reallocation of space.
6. The `while` loop again recursevely check for all next values (comma-separated) and then _normalise_ them (divide by 255){So that all values are within 0 to 1} and then push it to the vector. 
7. `inputs.push_back` moves the entire input image to the matrix.
8. `actuals.push_back` moves the entire one hot answer.
9. `count` is increased and thus a count is kept of how many samples are loaded