---
layout: post
title: Simple Memory Address to Decimal C++
date: 2015-05-25
modified: 2015-09-15
tags: [C++]
comments: true
pinned: true
image:
---

This program compares the memory addresses of two different variables on the stack and prints out the order of their addresses in decimal.

{% highlight cpp lineno=table lineanchors %}
// Comment
//
//  pointer_practice.cpp
//  Hello Pointer
//
//  Created by Yi Xia on 5/23/15.
//  Copyright (c) 2015 Yi Xia. All rights reserved.
//
 
#include <iostream>
#include <cmath>
#include <sstream>
#include <cstdlib>
 
using namespace std;
 
long hex_to_decimal(string s_num);
 
int main(int argc, const char * argv[]) {
    int val_1 = 10;
    int val_2 = 15;
    int *p_val_1 = &val_1;
    int *p_val_2 = &val_2;
    stringstream ss;
    ss << p_val_1;
    string s_1;
    ss >> s_1;
    ss.clear();
    ss << p_val_2;
    string s_2;
    ss >> s_2;
    cout << "val 1 address: " << s_1 << endl;
    cout << "val 2 address: " << s_2 << endl;
    long d_val_1 = hex_to_decimal(s_1);
    long d_val_2 = hex_to_decimal(s_2);
    cout << "val 1 address: " << d_val_1 << endl;
    cout << "val 2 address: " << d_val_2 << endl;
    if(d_val_1 > d_val_2){
        cout << "val 1 address is greater than val 2";
    }
    else{
        cout << "val 2 address is greater than val 1";
    }
    return 0;
}
 
long hex_to_decimal (string s_num){
//string s_num = to_string(num);
    long d_num = 0;
    char current;
    long base;
    for (int i = 2; i < s_num.length(); i++) {
        current = s_num.at(i);
        base = (long) pow(16, s_num.length()-1-i);
        switch (current) {
            case 'a':
                d_num += 10 * base;
                break;
            case 'b':
                d_num += 11 * base;
                break;
            case 'c':
                d_num += 12 * base;
                break;
            case 'd':
                d_num += 13 * base;
                break;
            case 'e':
                d_num += 14 * base;
                break;
            case 'f':
                d_num += 15 * base;
                break;
            default:
                d_num += (stoi(&current)) * base;
                break;
        }
    }
    return d_num;
}
{% endhighlight %}

Easier way for hex to decimal: 

{% highlight cpp %}
stringstream ss;
ss << p_val_1;
long add_1;
ss >> hex >> add_1;
{% endhighlight %}
