This repository contains Yandex packages for .NET Core

How to update:
--------------
1. Fork or branch this repo
2. Download actual .NET Core SDK and runtime from https://www.dot.net
3. Unpack downloaded archives to `/sdk/dotnet-*` and `runtime/dotnet-*` **NOTE: use Linux or MacOS to unpack - this will preserve file permissions**
5. Modify `debian/control` in `/sdk` and `/runtime`: use correct dependencies and versions in **Provides** and **(Pre-)Depends** sections (i.e. SDK package usually provides Runtime)
6. Modify `debian/install` and `debian/links` files for correct installation directories
7. Adjust `aspnetcore-store/debian/rules` and `aspnetcore-store/aspnetcore-store.csproj` for correct package versions
7. Build packages on **any TeamCity build agent** using `build.sh` script
8. Try installing packages on your dev machine
9. Create a pull request with your new changes, get approves and merge into Master
10. Build packages from Master branch on any build agent
11. Upload packages using `upload.sh` script
