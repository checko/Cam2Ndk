# Cam2Ndk
For Machine learning or images processing (`OpenCV`) applications on Android, it's often divided into two planes: part of it in Java and other part in `c++`(using NDK). There are various **Good** reasons that such applications should be implemented in native code(`c++` planes alone). With NDK Camera 2 APIs released as part of Android 7(`API version 24`) it has become a blessing for developers and delight for C/C++ lovers.

There are two parts to this repo:
1. **ndk_so:** Its a standalone `c++` code for camera control and there is no need to use Android Studio (c++ folks would surely love it), just build it from the command line. For this you need to download the version of NDK (cross compilation toolchain for android devices) you need (anything above `API version 24`) and set the appropriate path in the `Makefile`. Or if you already have NDK installed using Android Studio? It must be somewhere here -> `~/Library/Android/sdk/ndk/21.2.6472646` (on my macbook). 

Once you build the code it will generate `lib/libndksamplecam.so`. Drop this shared object to `jnilibs` folder, in ndk-cam project. Currently the `Makefile` is quite rudimentary and build for ABI type `arm64-v8a`, similarly more targets can be added. 

2. **ndk-cam:** This is merely a minimalistic boiler plate code to create `textureView` and render onto the screen. 


# Where do we capture Image? 
There is a callback function `imageCallback` inside the object `NDKCamera`, it gives you captured images for further processing, this image can further be converted to OpenCV `Mat` object or any other object that your frameworks requires. There is no Java -- C++ boundary to jump to and project delivery/shipping just by delivering shared object `.so` and `JAR` is not really required. 


# NDK Installation: 
To know what is NDK and how to install it, please follow the [article](https://medium.com/@tomdeore/opencv-on-android-tiny-with-optimization-enabled-932460acfe38), for us **Step-1** is only required. 
