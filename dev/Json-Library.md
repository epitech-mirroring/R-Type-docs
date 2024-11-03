---
title: Json Library
description: How to use the bundled Json library
published: false
date: 2024-11-03T17:23:00.000Z
tags: json, library
editor: markdown
dateCreated: 2024-11-03T17:00:00.000Z
---

# Json Library
## Introduction
The bundled Json Library is a custom-built library that provides a simple and efficient way to work with JSON data in 
your C++ projects. It is designed to be lightweight, easy to use, and compatible with a wide range of platforms.

## Features
- **Parsing**: The library can parse JSON data from strings or files, allowing you to read and manipulate JSON data easily.
- **Writing**: You can create JSON objects and arrays programmatically and write them to strings or files.
- **Accessing**: The library provides methods to access and modify JSON values, objects, and arrays.
- **Validation**: The library can validate JSON data against a schema to ensure its correctness.
- **Error Handling**: The library handles errors gracefully and provides detailed error messages to help you debug your code.

## Getting Started
To use the Json Library in your project, follow these steps:

### 1. Include the Library
The library is bundled with the project and can be included in your code by adding the following:

#### 1.1. Add the Conan Remote
If you are using Conan to manage your dependencies, add the following remote to your Conan configuration:

```bash
conan remote add Epitech-Mirroring https://nexus.place2die.com/repository/Epitech-Mirroring/
```

#### 1.2. Add the Dependency
Add the following dependency to your `conanfile.txt`:

```text
[requires]
stellar-forge-common/v0.1.0
```

### 1.3 (Optional). Setup CMake
If you are using CMake to build your project, add the following lines to your `CMakeLists.txt`:

```cmake
find_package(stellar-forge-common REQUIRED)
target_link_libraries(... PRIVATE stellar-forge-common::stellar-forge-common)
```

### 2. Use the Library
You can now use the Json Library in your code by including the necessary headers.

#### 2.1. Parsing JSON Data

```c++
#include <StellarForge/Common/json/JsonParser.hpp>
#include <StellarForge/Common/json/JsonObject.hpp>
#include <StellarForge/Common/json/JsonString.hpp>
#include <StellarForge/Common/json/JsonNumber.hpp>

int main() {
    json::JsonParser const parser;
    const auto *const data = parser.parse(R"({
        "name": "John Doe",
        "age": 30,
        "city": "New York"
    })");
    // Here you can access the data object
    // You know that the data object is a json::JsonObject
    // So you can cast it to a json::JsonObject
    const auto *const obj = dynamic_cast<const json::JsonObject *>(data);
    // Now you can access the fields of the object
    const auto *const name = obj->getValue<json::JsonString>("name");
    std::cout << "Name: " << name->getValue() << std::endl;
    
    // You can even check if a field exists
    if (obj->contains("country")) {
        const auto *const country = obj->getValue<json::JsonString>("country");
        std::cout << "Country: " << country->getValue() << std::endl;
    } else {
        std::cout << "Country field not found" << std::endl;
    }
    
    // Or check if a field is of a specific type
    if (obj->contains("age") && obj->getValue<json::IJsonObject>("age")->getType() == json::NUMBER) {
        const auto *const age = obj->getValue<json::JsonNumber>("age");
        // Numbers can be integers or floats
        // And you can check that with the isFloat() method
        if (age->isFloat()) {
            std::cout << "Age: " << age->getFloatValue() << std::endl;
        } else {
            std::cout << "Age: " << age->getIntValue() << std::endl;
        }
    } else {
        std::cout << "Age field not found or not a number" << std::endl;
    }
    return 0;
}
```

#### 2.2. Writing JSON Data

```c++
#include <StellarForge/Common/json/JsonParser.hpp>
#include <StellarForge/Common/json/JsonWriter.hpp>

int main() { 
    json::JsonParser const parser;
    const auto *const data = parser.parse(R"({
        "name": "John Doe",
        "age": 30,
        "city": "New York"
    })");
    
    std::ostringstream output;
    json::JsonWriter const writer(data);
    
    output << writer;
    return 0;
}
```

##### 2.2.1. You can also write JSON data with a pretty format

```c++
#include <StellarForge/Common/json/JsonParser.hpp>
#include "StellarForge/Common/json/JsonPrettyWriter.hpp"

int main() { 
    json::JsonParser const parser;
    const auto *const data = parser.parse(R"({
        "name": "John Doe",
        "age": 30,
        "city": "New York"
    })");
    
    std::ostringstream output;
    json::JsonPrettyWriter const writer(data);
    
    output << writer;
    return 0;
}
```

### 3. Read from a File
You can also read JSON data from a file using the `JsonReader` class:

```c++
#include <StellarForge/Common/json/JsonParser.hpp>
#include <StellarForge/Common/json/JsonReader.hpp>

int main() {
    auto const parser = json::JsonParser();
    json::JsonReader const reader(&parser);
    const json::IJsonObject *const tmp = reader << R"({
        "name": "John Doe",
        "age": 30,
        "city": "New York"
    })";
    
    // Here you can access the data object like in the previous examples
    
    // ...
    return 0;
}
```
