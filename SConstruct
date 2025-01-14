
import os
PLATFORM = Platform()
DEBUG = ARGUMENTS.get("debug", 0)

if 'CUDA_PATH' in os.environ:
    CUDA_INCLUDE_PATH = os.environ['CUDA_PATH'] + "/include"
else:
    CUDA_INCLUDE_PATH = ""

ENV = Environment(CPPPATH = ['.', "./contrib/"+PLATFORM.name+"/oidn/include", "./contrib/win/OpenImageIO/include" if PLATFORM.name == "win32" else "", CUDA_INCLUDE_PATH, "/opt/homebrew/include" if PLATFORM.name == "darwin" else ""
],
                  CCFLAGS="-std=c++11"+ (" /EHsc" if PLATFORM.name == "win32" else ""))

# Used for debbugging
if int(DEBUG):
    ENV.Append(CCFLAGS=' -ggdb3')

SOURCES = Glob("src/*.cpp")

LIBPATH = []
if PLATFORM.name == "win32":
    LIBPATH.append("./contrib/win/oidn/lib")
    LIBPATH.append("./contrib/win/OpenImageIO/lib")
elif PLATFORM.name == "darwin":
    LIBPATH.append("./contrib/darwin/oidn/lib")
    LIBPATH.append("/opt/homebrew/lib")
    
LIBS = []
LIBS.append("OpenImageDenoise")
LIBS.append("OpenImageIO")

LINKFLAGS = []
if PLATFORM.name == "darwin":
    LINKFLAGS.append("-Wl,-rpath,.")

if PLATFORM.name == "win32":
    ENV.Append(CPPDEFINES = "NOMINMAX")

    # Copy over the OIDN dlls to the bin directory
    ENV.Command("bin/OpenImageDenoise.dll", "./contrib/win/oidn/bin/OpenImageDenoise.dll", Copy("$TARGET", "$SOURCE"))
    ENV.Command("bin/tbb12.dll", "./contrib/win/oidn/bin/tbb12.dll", Copy("$TARGET", "$SOURCE"))

    # Copy all of OIIO many dependencies!
    ENV.Command("bin/boost_atomic-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_atomic-vc141-mt-x64-1_67.dll", Copy("$TARGET", "$SOURCE"))
    ENV.Command("bin/boost_chrono-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_chrono-vc141-mt-x64-1_67.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/boost_container-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_container-vc141-mt-x64-1_67.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/boost_context-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_context-vc141-mt-x64-1_67.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/boost_coroutine-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_coroutine-vc141-mt-x64-1_67.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/boost_date_time-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_date_time-vc141-mt-x64-1_67.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/boost_filesystem-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_filesystem-vc141-mt-x64-1_67.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/boost_math_c99-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_math_c99-vc141-mt-x64-1_67.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/boost_math_c99f-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_math_c99f-vc141-mt-x64-1_67.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/boost_math_c99l-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_math_c99l-vc141-mt-x64-1_67.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/boost_math_tr1-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_math_tr1-vc141-mt-x64-1_67.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/boost_math_tr1f-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_math_tr1f-vc141-mt-x64-1_67.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/boost_math_tr1l-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_math_tr1l-vc141-mt-x64-1_67.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/boost_random-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_random-vc141-mt-x64-1_67.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/boost_regex-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_regex-vc141-mt-x64-1_67.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/boost_system-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_system-vc141-mt-x64-1_67.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/boost_thread-vc141-mt-x64-1_67.dll", "./contrib/win/OpenImageIO/bin/boost_thread-vc141-mt-x64-1_67.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/Half.dll", "./contrib/win/OpenImageIO/bin/Half.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/Iex-2_2.dll", "./contrib/win/OpenImageIO/bin/Iex-2_2.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/IexMath-2_2.dll", "./contrib/win/OpenImageIO/bin/IexMath-2_2.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/IlmImf-2_2.dll", "./contrib/win/OpenImageIO/bin/IlmImf-2_2.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/IlmImfUtil-2_2.dll", "./contrib/win/OpenImageIO/bin/IlmImfUtil-2_2.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/IlmThread-2_2.dll", "./contrib/win/OpenImageIO/bin/IlmThread-2_2.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/Imath-2_2.dll", "./contrib/win/OpenImageIO/bin/Imath-2_2.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/jpeg62.dll", "./contrib/win/OpenImageIO/bin/jpeg62.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/libeay32.dll", "./contrib/win/OpenImageIO/bin/libeay32.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/libpng16.dll", "./contrib/win/OpenImageIO/bin/libpng16.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/lzma.dll", "./contrib/win/OpenImageIO/bin/lzma.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/OpenImageIO.dll", "./contrib/win/OpenImageIO/bin/OpenImageIO.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/OpenImageIO_Util.dll", "./contrib/win/OpenImageIO/bin/OpenImageIO_Util.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/ssleay32.dll", "./contrib/win/OpenImageIO/bin/ssleay32.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/tiff.dll", "./contrib/win/OpenImageIO/bin/tiff.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/tiffxx.dll", "./contrib/win/OpenImageIO/bin/tiffxx.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/turbojpeg.dll", "./contrib/win/OpenImageIO/bin/turbojpeg.dll", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/zlib1.dll", "./contrib/win/OpenImageIO/bin/zlib1.dll", Copy("$TARGET","$SOURCE"))
elif PLATFORM.name == "darwin":
    ENV.Command("bin/libOpenImageDenoise.1.4.0.dylib", "./contrib/darwin/oidn/lib/libOpenImageDenoise.1.4.0.dylib", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/libOpenImageDenoise.1.dylib", "./contrib/darwin/oidn/lib/libOpenImageDenoise.1.dylib", Copy("$TARGET","$SOURCE"))
    ENV.Command("bin/libOpenImageDenoise.dylib", "./contrib/darwin/oidn/lib/libOpenImageDenoise.dylib", Copy("$TARGET","$SOURCE"))
    
    
program = ENV.Program(target="bin/Denoiser", source=SOURCES,
                              LIBPATH=LIBPATH, LIBS=LIBS, LINKFLAGS=LINKFLAGS)

