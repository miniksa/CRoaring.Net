# CRoaring.Net
[![MyGet](https://img.shields.io/myget/rogueexception/vpre/CRoaring.Net.svg)](https://www.myget.org/feed/rogueexception/package/nuget/CRoaring.Net) 
[![Build status](https://ci.appveyor.com/api/projects/status/b2no6fcbpr8g6bi2?svg=true)](https://ci.appveyor.com/project/RogueException/croaring-net)

A .Net wrapper for [CRoaring](https://github.com/RoaringBitmap/CRoaring) - a C implementation of [RoaringBitmap](https://github.com/RoaringBitmap/RoaringBitmap).

## Usage
```cs
using (var rb1 = new RoaringBitmap())
using (var rb2 = new RoaringBitmap())
{
	rb1.AddMany(1, 2, 3, 4, 5, 100, 1000);
	rb1.Optimize();
	
	rb2.AddMany(3, 4, 5, 7, 50);
	rb2.Optimize();

	using (var result = rb1.And(rb2))
	{
		Console.WriteLine(result.Contains(2));
		Console.WriteLine(result.Contains(4));
		Console.WriteLine(result.Contains(5));
	}
}
```

## Project Notes
- CRoaring is a C/C++ dummy project whose whole responsibility is to trigger VCpkg to build the CRoaring native library.
- CRoaring.Net is a .Net Core 8 project that wraps the native library using P/Invoke which works on Linux and Windows.
  - It will copy the binaries out of the native VCpkg project folder as content assets into its own output directory.

## Compiling
### Linux
Requirements:
- [GCC](https://gcc.gnu.org/)

Run the `build.sh` script

### Windows
Requirements:
- [VS2022 or later](https://www.visualstudio.com/downloads/)
- [VCpkg](https://vcpkg.io/en/getting-started) and please do `vcpkg integrate install`. (CMake for CRoaring will be handled by VCpkg on your behalf.)

Build the CRoaring and CRoaring.Net projects.

## Testing CRoaring.Net

Run the `test.sh` or `test.bat` scripts.
