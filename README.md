# BaseCUDA

A C++ base program that runs CUDA adjusted code on a NVIDIA GPU.

I don't know how to build programs on a GPU, but eventually I'll be able to recreate this program from scratch.

Things that make sense to me:
1. arraySize, a[], and b[] are treated as consts.
2. c[] will hold the summed values in a + b.
3. cudaStatus is set to the return value of addWithCuda() given (the array that will hold the results, a[], b[], and the const arraySize).
3a. The addWithCuda() function sets the three device pointers to 0 and creates a cudaError_t object.
3b. Sets the cudaError_t object to the result of cudaSetDevice(0)
3b1. cudaSetDevice(0)'s code is hidden...
3c. The following condition checks to see if the result is not equal to cudaSuccess, which then return's an error.
3d. The cudaError_t object is set to a few other functions like... (cudaMalloc for c, cudaMalloc for a, cudaMalloc for b, cudaMemcpy for
    dev_a and dev_b pointers.
3e. addKernel<<<1, size>>>() launches code on the GPU with one thread for each element.
3f. cudaError_t object is set to gudaGetLastError() which checks for any errors launching the kernel.
3g. cudaError_t object is set to cudaDeviceSynchronize() which waits for the code to finish, and returns any errors encountered.
3h. cudaError_t object is et to the cudaMemcpy() which copies the code's output from the GPU buffer to the CPU's/Host memory.
*In each of the conditionals from 3b - 8 if they were not successful then the device pointers' memory are freed and the status
    (aka cudaError_t object is returned.
4. Going back to main(), conditional checks to see if the operation was a success.
5. If it is the result is printed to the console screen.
6. cudaError_t object is set to cudaDeviceReset() which clears up the GPU.
7. My screen pauser occurs...
8. Program ends!

More on this later!
