gcc="clang"
gpp="clang++"

main: 
	gcc -pthread -O3 -mavx -mavx2 -mfma -mf16c -c ./whisper.cpp/ggml.c -fPIC
	gcc -pthread -O3 -mavx -mavx2 -mfma -mf16c -c ./whisper.cpp/whisper.cpp -fPIC
	g++ -pthread -O3 -std=c++11 -c ./main.cpp -fPIC
	g++ -pthread -o ./libwhisper.so ./whisper.o ./ggml.o ./main.o --shared -static-libstdc++ -fPIC -lstdc++

install:
	sudo cp *.so /usr/lib/
	
gcc="$(HOME)/Android/Sdk/ndk/24.0.8215888/toolchains/llvm/prebuilt/linux-x86_64/bin/aarch64-linux-android21-clang"
gpp="$(HOME)/Android/Sdk/ndk/24.0.8215888/toolchains/llvm/prebuilt/linux-x86_64/bin/aarch64-linux-android21-clang++"

compile.android:
	$(gcc) -O3 -std=c11 -pthread -fPIC -c ./whisper.cpp/ggml.c
	$(gpp) -O3 -std=c++11 -pthread -fPIC -c ./whisper.cpp/whisper.cpp
	$(gpp) -O3 -std=c++11 -pthread -fPIC -c ./main.cpp
	$(gpp) -o ./libwhisper_android.so ./whisper.o ./ggml.o ./main.o --shared -static-libstdc++ -fPIC 


# clean up the directory
clean:
	rm -f *.o main *.so