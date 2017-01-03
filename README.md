# BaseCUDA

A C++ base program that runs CUDA adjusted code on a NVIDIA GPU.
<br><br>
I don't know how to build programs on a GPU, but eventually I'll be able to recreate this program from scratch.
<br><br>
Things that make sense to me:
<ol>
<li> arraySize, a[], and b[] are treated as consts.
<br><li> c[] will hold the summed values in a + b.
<br><li> cudaStatus is set to the return value of addWithCuda() given (the array that will hold the results, a[], b[], and the const arraySize).
<ol>
<br><li> The addWithCuda() function sets the three device pointers to 0 and creates a cudaError_t object.
<br><li> Sets the cudaError_t object to the result of cudaSetDevice(0)
<br><li> cudaSetDevice(0)'s code is hidden...
<br><li> The following condition checks to see if the result is not equal to cudaSuccess, which then return's an error.
<br><li> The cudaError_t object is set to a few other functions like... (cudaMalloc for c, cudaMalloc for a, cudaMalloc for b, cudaMemcpy for
    dev_a and dev_b pointers.
<br><li> addKernel<<<1, size>>>() launches code on the GPU with one thread for each element.
<br><li> cudaError_t object is set to gudaGetLastError() which checks for any errors launching the kernel.
<br><li> cudaError_t object is set to cudaDeviceSynchronize() which waits for the code to finish, and returns any errors encountered.
<br><li>cudaError_t object is et to the cudaMemcpy() which copies the code's output from the GPU buffer to the CPU's/Host memory.
</ol>
<br>*In each of the conditionals from 3b - 8 if they were not successful then the device pointers' memory are freed and the status
    (aka cudaError_t object is returned.
<br><li> Going back to main(), conditional checks to see if the operation was a success.
<br><li> If it is the result is printed to the console screen.
<br><li> cudaError_t object is set to cudaDeviceReset() which clears up the GPU.
<br><li> My screen pauser occurs...
<br><li> Program ends!
</ol>
<br><br>
More on this later!
