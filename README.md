# librdkafka NuGet Package for vcpkg

[![Build librdkafka NuGet Package](https://github.com/darioajr/librdkafka-vcpkg-nuget/actions/workflows/build-nuget.yml/badge.svg)](https://github.com/darioajr/librdkafka-vcpkg-nuget/actions/workflows/build-nuget.yml)
[![NuGet](https://img.shields.io/nuget/v/librdkafka.vcpkg.svg)](https://www.nuget.org/packages/librdkafka.vcpkg/)

This repository provides a pre-built NuGet package of **librdkafka** (Apache Kafka C/C++ client library) compiled with vcpkg for Windows x64 using Visual Studio 2022 (vc143).

## Features

- ✅ Pre-compiled librdkafka binaries for Windows x64
- ✅ Both static libraries (.lib) and dynamic libraries (.dll)
- ✅ Debug and Release configurations
- ✅ Automatic MSBuild integration via .targets file
- ✅ Headers included for C and C++ development
- ✅ Built with vcpkg for consistent dependency management

## Installation

### Via NuGet Package Manager
```
Install-Package librdkafka.vcpkg
```

### Via Package Manager Console
```
PM> Install-Package librdkafka.vcpkg
```

### Via .NET CLI
```bash
dotnet add package librdkafka.vcpkg
```

## Usage

Once installed, the package automatically configures your Visual Studio project with:

- **Include directories**: Headers are automatically added to your project
- **Library directories**: Static libraries are linked automatically
- **Dependencies**: Required libraries (`rdkafka.lib`, `rdkafka++.lib`) are linked
- **Runtime files**: DLLs are copied to output directory during build

### Example C++ Code

```cpp
#include <librdkafka/rdkafka.h>
#include <iostream>

int main() {
    rd_kafka_conf_t *conf = rd_kafka_conf_new();
    
    // Configure Kafka client
    rd_kafka_conf_set(conf, "bootstrap.servers", "localhost:9092", nullptr, 0);
    
    // Create producer instance
    char errstr[512];
    rd_kafka_t *producer = rd_kafka_new(RD_KAFKA_PRODUCER, conf, errstr, sizeof(errstr));
    
    if (!producer) {
        std::cerr << "Failed to create producer: " << errstr << std::endl;
        return 1;
    }
    
    std::cout << "Kafka producer created successfully!" << std::endl;
    
    rd_kafka_destroy(producer);
    return 0;
}
```

## Version Information

- **librdkafka version**: 2.10.1
- **Target platform**: Windows x64
- **Compiler**: Visual Studio 2022 (vc143)
- **vcpkg**: Latest stable

## Build Configuration

The package includes:

### Static Libraries (Release)
- `rdkafka.lib`
- `rdkafka++.lib`

### Static Libraries (Debug)
- `rdkafka.lib` (debug version)
- `rdkafka++.lib` (debug version)

### Dynamic Libraries (Release)
- `rdkafka.dll`
- `rdkafka++.dll`

### Dynamic Libraries (Debug)
- `rdkafka.dll` (debug version)
- `rdkafka++.dll` (debug version)

## Requirements

- Windows 10/11 x64
- Visual Studio 2019 or later
- .NET Framework 4.7.2 or later / .NET Core 3.1 or later

## Contributing

1. Fork this repository
2. Make your changes
3. Test the build pipeline
4. Submit a pull request

## Build from Source

To build the package locally:

```bash
# Clone the repository
git clone https://github.com/darioajr/librdkafka-vcpkg-nuget.git
cd librdkafka-vcpkg-nuget

# Install vcpkg dependencies
vcpkg install --triplet x64-windows

# Pack the NuGet package
nuget pack librdkafka.nuspec
```

## License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

The librdkafka library itself is also licensed under the Apache License 2.0.

## Links

- [librdkafka GitHub Repository](https://github.com/confluentinc/librdkafka)
- [Apache Kafka](https://kafka.apache.org/)
- [vcpkg](https://github.com/Microsoft/vcpkg)
- [NuGet Package](https://www.nuget.org/packages/librdkafka.vcpkg/)

## Support

For issues related to this NuGet package, please open an issue on this repository.

For librdkafka-specific issues, please refer to the [official librdkafka repository](https://github.com/confluentinc/librdkafka).
