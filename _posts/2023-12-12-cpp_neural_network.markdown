---
layout: post
title: Neural Network from scratch
project_length: "2/5"
date: 2023-12-12 00:00:00 +0300
description: In this project, as the final coursework for TW3720TU, I, alongside my group, worked to code neural networks from scratch (in C++). The main goal was to practice our object-oriented programming skills in C++, which we had learned through the computer science course called Object-Oriented Scientific Programming with C++.
img: neural-networks-background.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [C++, OOP] # add tag
---

In this project, as the final coursework for TW3720TU, I, alongside my group, worked to code neural networks from scratch (in C++). The main goal was to practice our object-oriented programming skills in C++, which we had learned through the course called Object-Oriented Scientific Programming with C++.

To begin a Matrix class was created using templates. This alows the class to work with any input. 

```cpp
template <typename T>
class Matrix {...
};
```

Overloading operators for '+', '-', and '*' (for both scalar and matrix multiplication) were created in order to perform matrix operations on the new class intuitively.




```cpp
Matrix<double> m1(2, 2, {1.0, 2.0, 3.0, 4.0});
Matrix<double> m2(2, 2, {5.0, 6.0, 7.0, 8.0});

Matrix<double> result = m1 + m2;
Matrix<double> scaled = m1 * 2.0;
```

The ANN was consequently created, first a layer class was defined with virtual functions: 

```cpp
template<typename T>
class Layer
{
    public:
        virtual Matrix<T> forward(const Matrix<T>& x) = 0;
        virtual Matrix<T> backward(const Matrix<T>& dy) = 0;
};
```

This was done so that they could then be implemented by derived classes (Linear and RelU) for a specific behaviour for each type of layer:

Example of forward pass in ReLU:
```cpp
        virtual Matrix<T> forward(const Matrix<T>& x) override final 
        {
            // Calculate the forward pass
            Matrix<T> y = Matrix<T>(n_samples, out_features);
            for (int i = 0; i < n_samples; i++) 
            {
                for (int j = 0; j < out_features; j++) 
                {
                    if (x.data[i][j] > 0) 
                    {
                        y.data[i][j] = x.data[i][j];
                    }
                    else 
                    {
                        y.data[i][j] = 0;
                    }
                }
            }
            // Store the input matrix in the cache
            this->cache.data = x.data;

            // Return the output matrix
            return y;
        }
```

example in forward pass in Linear: 

```cpp
        //Forward pass
        virtual Matrix<T> forward(const Matrix<T>& x) override final 
        {
                // Generate output matrix
                Matrix<T> y = Matrix<T>(n_samples, out_features);

                // Calculate the forward pass
                y = x * Weights + Bias;

                // Store cache
                this->cache.data = x.data;

                // Return Output
                return y;
        }
```

MSEloss, MSEgrad, argmax and other functions were used in order to optimize the linear function and finally the Net class was used as the final Neural Network.

For more information about the project please consult me for acess to the private repository.