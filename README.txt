Note:

git branch -m jetson-orin main
git fetch origin
git branch -u origin/main main
git remote set-head origin -a



STEP 1) Install lib971apriltag.so 
This is 971's cuda apriltag library wrapped for photonvision.

to compile on a fresh jetpack 6.2 install:
sudo apt install openjdk-17-jdk

#add the following 3 lines to .bashrc
export PATH=$PATH:/usr/local/cuda/bin
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/lib64
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-arm64/


git clone https://github.com/wpilibsuite/allwpilib.git
cd allwpilib
sudo apt install openjdk-17-jdk
sudo apt install ninja-build
sudo apt install protobuf-compiler
sudo apt install libxrandr-dev
sudo apt install libssh-dev
sudo apt install libopencv4.5-java
cmake --preset default -DWITH_GUI=OFF -DWITH_JAVA=ON -DWITH_SIMULATION_MODULES=OFF -DWITH_TESTS=OFF -DOPENCV_JAR_FILE=/usr/share/java/opencv.jar
cd build-cmake 
cmake --build . --parallel 4  #may run out of memory compiling wpimath if too high
sudo cmake --build . --target install

cd ..
git clone https://github.com/FRC-Team-4143/GpuDetectorJNI.git
cd GpuDetectorJNI
cd third_party/apriltag
mkdir build
cd build
cmake ..
make
cd ../../..
mkdir build
cd build
cmake ..
make
sudo cp lib971apriltag.so /usr/lib 

STEP 2)
Git clone this repo.  
https://github.com/Barlow-Robotics/2026-PhotonVision-TEST
cd 2026-PhotonVision-TEST
Use build instructions in photonvision: https://docs.photonvision.org/en/v2026.1.1/docs/contributing/building-photon.html.

Use ./gradlew shadowJar 
Then find the jar file & run. 
