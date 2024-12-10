# Installation

## Prerequisites

Make sure your C++ version >= C++17.

## Download the source code

`git clone` the project, then you'll have some options to compile:

### Using Makefile

```bash
make
```

### Using g++

Compile all files inside `src/` directory:

```bash
g++ src/*.cpp main -std=c++17
```

## Using prebuild

### Executable

- Go to [The Release page](https://github.com/khongsomeo/GPA-OOP/releases).
- Find your favourite version, then download the `release.zip` file.
- Unzip and use!

### Docker container

```bash
docker pull ghcr.io/khongsomeo/gpa-oop:latest
```
