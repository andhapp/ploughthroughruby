
---
layout: post
title: Installing ffi 1.11.1 on Mojave
date_string: 27 September 2019
---

If you've installed to Mojave and are frustrated by the errors you get on installing ffi (1.11.1), then this blog 
post is for you.

I had the same issue last week and after trawling through the internet and trying every possible suggestion, one finally
worked!

But, before that, a little discussion on the actual error is in order. Below is a small snippet of the actual error on `bundle install`:

```
Configuring libffi for i386
configure: error: in `/Users/andhapp/Projects/github/startup/pimful/vendor/ruby/2.6.0/gems/ffi-1.11.1/ext/ffi_c/libffi-i386':
configure: error: C compiler cannot create executables
See `config.log' for more details
make[1]: *** No targets specified and no makefile found.  Stop.
make: *** ["/Users/andhapp/Projects/github/startup/pimful/vendor/ruby/2.6.0/gems/ffi-1.11.1/ext/ffi_c"/libffi-i386/.libs/libffi_convenience.a] Error 2
```

`libffi` is trying to configure for i386 architecture. Mojave doesn't support that architecture, so the actual linking file is missing. A peek into the 
`config.log` reveals that fact:

```
ld: warning: The i386 architecture is deprecated for macOS (remove from the Xcode build setting: ARCHS)
ld: warning: ignoring file /Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/lib/libSystem.tbd, missing required architecture i386 in file /Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/usr/lib/libSystem.tbd
ld: dynamic main executables must link with libSystem.dylib for architecture i386
clang: error: linker command failed with exit code 1 (use -v to see invocation)
```

There are several suggestion to actually link the file present in Mojave and make the missing file available that way, but that doesn't work either.

After several frustrating hours, the following suggestion worked perfectly:

```
brew reinstall libffi

export LDFLAGS="-L/usr/local/opt/libffi/lib"
export PKG_CONFIG_PATH="/usr/local/opt/libffi/lib/pkgconfig"
```

Reinstallation of `libffi` installs it correctly for Mojave and then `bundle install` works like a charm.


Hope it helps!
