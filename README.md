# LFS-history-describe
Small explanation and troubleshooting of my custom LFS.
# My Linux From Scratch (LFS) 

##  Current Status
- **Temporary Toolchain:** Successfully compiled cross-compiler and temporary glibc (Pass 1 & Pass 2).
- **Environment Isolation:** Configured the `chroot` environment and mounted virtual kernel filesystems (`/dev`, `/proc`, `/sys`).
-  **Basic System Software:** Currently in the final stages (Chapter 8). Working through complex dependency resolutions, currently troubleshooting the `Perl` package compilation.

## Main challenges 

* **Dependency Hell (GCC & Glibc):** I had to rebuild the GCC compiler ~10 times due to cyclic dependencies between static (`.a`) and dynamic (`.so`) libraries. It taught me how the dynamic linker (`ld.so`) actually resolves paths in memory.
* **The API Contract (Linux Headers):** I learned the hard way that incompletely assembled Linux headers will break downstream compilations (like `bison` and `python`). It proved that infrastructure layers must have strict, reliable API contracts.
* **The Illusion of chroot & Need for Containers:** During compilation, I temporarily used a "dirty hack" by creating hardlinks to my host OS libraries to force a build. This broke my `chroot` isolation, causing scripts (like Perl's `Configure`) to mix host and LFS environments and fail. **This painful mistake gave me a profound, practical understanding of why the industry moved to Docker** — I now truly understand why Namespaces and Cgroups are absolutely critical for guaranteeing environment isolation.


