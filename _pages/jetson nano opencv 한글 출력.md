---
title: "jetson nano에서 opencv한글출력(C++)"
excerpt: "jetson nano에서 opencv contrib(freetype2, harfbuzz)포함하여 빌드하기 - 한글 출력"
permalink: /develop/intern2
layout: category
---




# jetson nano에서 opencv contrib(freetype2, harfbuzz)포함하여 빌드하기 - 한글 출력

1. freetype2를 다운받는다.(tar.bz2 압축풀기 : tar -xvf *파일명*)

   다운 링크 : https://sourceforge.net/projects/freetype/files/freetype2/

   cmake로 freetype2를 빌드해준다. (빌드시에는 다운받은 폴더와 다른 위치에서!)

   `cmake [압축 풀고 cmakelist 파일 있는 경로]`

   ![intern6](C:\Users\JH\Desktop\project\lhju4e.github.io\images\intern6.png)

2. harfbuzz를 다운받는다.

   다운 링크 : https://www.freedesktop.org/software/harfbuzz/release/

   cmake로 harfbuzz를 빌드해준다.(위와 동일)

3. opencv-contrib-3.3.1을 다운받는다. (*3.3.1은 사용자 버전에 맞춰서 변경*)

   https://github.com/opencv/opencv_contrib

   https://github.com/opencv/opencv_contrib/releases/tag/3.3.1

   (opencv 3.3.1 release 버전으로 맞춰서 다운 받아야 함)

   README처럼 옵션을 줘서 해도 되겠지만 확실하게 하기위해 module에 필요한 모듈 빼고 다 지워준다.

4. opencv재빌드를 한다.

   소스파일이 있으면 cmakelist만 넣어서 해줘도 되겠지만 못찾으면 그냥 https://jkjung-avt.github.io/opencv-on-nano/ 여기서 스크립트 파일 받아서 실행. 

   그냥 통으로 opencv받아서 하면 6기가 이상 날아감.

   sh 파일은 경로 아무데서 실행해도 상관 없음.

   **스크립트 파일 수정부분 : 버전, cmake에서 -D OPENCV_EXTRA_MODULES_PATH=/home/ubuntu/opencv_contrib-3.3.1/modules (3에서 받은 opencv_contrib/modules 폴더 경로)**

   *여기서의 사용 버전은 3.3.1*

   

   이전에 사용했던 스크립트 : 

   cmake -D CMAKE_BUILD_TYPE=RELEASE **-D OPENCV_EXTRA_MODULES_PATH=/home/ubuntu/opencv_contrib/modules** -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_CUDA=ON -D CUDA_ARCH_BIN="5.3" -D CUDA_ARCH_PTX="" -D WITH_CUBLAS=ON -D ENABLE_FAST_MATH=ON -D CUDA_FAST_MATH=ON -D ENABLE_NEON=ON -D WITH_GSTREAMER=ON -D WITH_LIBV4L=ON -D BUILD_opencv_python2=ON -D BUILD_opencv_python3=ON -D BUILD_TESTS=OFF -D BUILD_PERF_TESTS=OFF -D BUILD_EXAMPLES=OFF -D WITH_QT=ON -D WITH_OPENGL=ON **opencv/**

   

5. make -j3

   sudo make install

   sudo ldconfig

   
   *opencv버전 확인* : `pkg-config --modversion opencv`


   빌드가 정상이라면 이렇게 freetype2와 harbuzz가 yes라고 나옴

   

   ![intern7](C:\Users\JH\Desktop\project\lhju4e.github.io\images\intern7.png)

   

   *빌드중에 이런 에러가 나오면 로그대로 cuda_gl ... .h로 가서 수정*

   ![intern8](C:\Users\JH\Desktop\project\lhju4e.github.io\images\intern8.png)

   

   *오른쪽 사진과 같이 주석처리*

   ![intern9](C:\Users\JH\Desktop\project\lhju4e.github.io\images\intern9.png)

   

