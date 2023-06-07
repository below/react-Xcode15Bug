# react-Xcode15Bug
A bug in react-native when building with Xcode 15

## Description

When building with Xcode 15 Beta 1, building fails with a C++ issue in boost:

```
› Compiling react-native Pods/RCT-Folly » json.cpp

❌  (ios/Pods/boost/boost/container_hash/hash.hpp:131:33)

  129 | #else
  130 |         template <typename T>
> 131 |         struct hash_base : std::unary_function<T, std::size_t> {};
      |                                 ^ no template named 'unary_function' in namespace 'std'; did you mean '__unary_function'?
  132 | #endif
  133 | 
  134 |         struct enable_hash_value { typedef std::size_t type; };

```

Apparently, boost 1.8x does not have this issue and builds correctly. However, react-jsi currently does not work with boost 1.8x due to breaking changes.

## Steps to reproduce

* Prerequisite: On a machine running macOS, ensure that [Xcode 15](https://developer.apple.com/download/all/?q=xcode%2015) is installed
* Download or clone this [Sample](https://github.com/below/react-Xcode15Bug)
* `cd react-Xcode15Bug`
* `npm install && (cd ios && pod install)`

Then either:
* `yarn ios`

Or
* `xed ios` and build with Xcode
