- Python-based deep learning library that runs on CPU by default and supports GPU acceleration using CUDA. It follows a define-by-run approach, creating dynamic computation graphs during execution, which makes debugging and customization easier.
	- Uses dynamic graphs for flexibility
	- Provides automatic differentiation for gradient computation
	- Supports GPU acceleration with CUDA
- ![[Pasted image 20260823143934.png]]
- Can be installed on Windows using pip for CPU (without GPU):
	- ```python
	  pip install torch torchvision torchaudio
	  ```
- Install in notebooks (Jupyter Notebook or Google Colab):
	- ```python
	  !pip install torch torchvision torchaudio
	  ```
- **PyTorch Tensors**
	- Tensors are the fundamental data structures in PyTorch, similar to NumPy arrays but with GPU acceleration capabilities. PyTorch tensors support automatic differentiation, making them suitable for deep learning tasks.
	- ```python
	  import torch
	  
	  x = torch.tensor([1.0, 2.0, 3.0])
	  print('1D Tensor: \n', x)
	  y = torch.zeros((3, 3))
	  print('2D Tensor: \n', y)
	  ```
	- ![[Pasted image 20260823145147.png]]
- **Operations on Tensors**
	- ```python
	  a = torch.tensor([1.0, 2.0])
	  b = torch.tensor([3.0, 4.0])
	  print('Element Wise Addition of a & b: \n', a + b)
      print('Matrix Multiplication of a & b: \n',
	        torch.matmul(a.view(2, 1), b.view(1, 2)))
	  ```
	  - ![[Pasted image 20260823145523.png]]
  - **Reshaping and Transposing Tensors**
	  - Both reshape() and view() change the shape of a tensor without changing its data. However, view() requires the tensor to be stored contiguously in memory, while reshape() can handle more cases by creating a copy when necessary.
	  - ```python
	    import torch
	    t = torch.tensor([[1, 2, 3, 4],
						  [5, 6, 7, 8],
						  [9, 10, 11, 12]])
	    print("Reshaping")
	    print(t.reshape(6, 2))
	    print("\nTransposing")
	    print(t.tranpose(0, 1))
	    ```
	    - ![[Pasted image 20260823150116.png]]
- **Autograd & Computational Graphs**
	- Autograd module automates gradient calculation for backpropagation. This is important in training deep neural networks.
	- ```python
	  x = torch.tensor(2.0, requires_grad=True)
	  y = x ** 2
	  y.backward()
	  print(x.grad) # output is tensor(4.)
	  # y = x ** 2 computes the square of x and records the operation
	  # in the computational graph. y.backward() performs backpropagation and calculates the gradient of y with respect to x. Since y = x^2, its derivative is dy/dx = 2x. For x = 2, the gradient is 2 x 2 = 4, which is stored in x.grad.
	  ```
	  - PyTorch dynamically creates a computational graph that tracks operations and gradients for backpropagation.