---
title: "C/C++ dev env setup on windows with VS Code"
date: 2024-07-18
---

There are multiple ways to setup C/C++ dev environment on windows 11 using VS Code.

1. [Using MinGW-x64](https://www.youtube.com/watch?v=AgDlL1Ysm34)
2. [Using MinGW-x64, MSYS2 tool chains](https://code.visualstudio.com/docs/cpp/config-mingw).
3. [Using Visual Studio C++ development workload](https://code.visualstudio.com/docs/cpp/config-msvc)
4. [Using WSL, linux distribution with VS Code](https://code.visualstudio.com/docs/cpp/config-wsl)

Important consideration on choosing which option to choose depends on - if you need to build for running the application on windows or linux. If the answer is :
- **Windows**, choose the 1st, 2nd or 3rd approach. 
- **Linux**, choose the 4th approach of WSL.

The one that I prefer is 4th option, as its for running application on Linux which is widely used for container based workloads.

**Note:** After the setup, F5 can be used to run the ```main.c``` or ```main.cpp``` files. Just choose the g++ option using that both .c and .c++ files can be run. gcc option only runs .c files and thows error for .c++ files.