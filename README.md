# Chromium DevTools Remote

Chromium DevTools remote for C++.

## Example

Example printing to PDF.

```c++
#include <boost/asio.hpp>
#include <chrome_remote/chrome_remote.h>

int main(int, char* [])
{
  boost::asio::io_service io;

  /* RAII wrapper over a headless chromium process */
  chrome_remote::Browser browser{io};

  /* Chromium DevTools remote */
  chrome_remote::Remote remote{io};

  browser.ready()
    .then(remote.connect(browser))
    .then(chrome_remote::print_to_pdf(
      remote, "http://www.example.com", "example.pdf"))
    .done();

  io.run();
  return 0;
}
```

## Use with Conan

```sh
# Install conan
python -m pip install --user --upgrade conan

# Add signal9's repository
~/.local/bin/conan remote add signal9 https://api.bintray.com/conan/signal9/conan
```

Include in your `conanfile.txt`.

```txt
[requires]
chrome_remote/1.1.1@signal9/stable

[generators]
cmake
```

See also [Conan - Getting Started](http://docs.conan.io/en/latest/getting_started.html).

## Build (Development)

```sh
# Install conan
python -m pip install --user --upgrade conan

# Add signal9's repository
~/.local/bin/conan remote add signal9 https://api.bintray.com/conan/signal9/conan

# Create build dir
mkdir stage && cd stage

# Install conan dependencies
~/.local/bin/conan install -r signal9 ..

# Configure and build
cmake ..
cmake --build .
```

## Dependencies

* Conan (can be installed via `pip`)
* CMake
* Boost
