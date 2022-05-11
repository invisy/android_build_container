# Android build container

The Dockerfile in this directory sets up an Ubuntu Trusty image ready to build a variety of Android branches (>= Lollipop). Original Google`s Dockerfile you can found [here](https://android.googlesource.com/platform/build/+/master/tools/docker/Dockerfile).

## Build

### Copy your host gitconfig, or create a stripped down version.
```bash
cp ~/.gitconfig gitconfig
```
### Build the image:
```bash
docker build --build-arg userid=$(id -u) --build-arg groupid=$(id -g) --build-arg username=$(id -un) -t android-build-trusty .
```
or if you use docker on Windows you can use next command:
```bash
docker build --build-arg userid=1000 --build-arg groupid=1000 --build-arg username=my_username -t android-build-trusty .
```

## Usage example

You can use it in Docker on Windows. Next command allows to mount external hard drive partition to WSL.
```bash
wsl --mount \\.\PHYSICALDRIVE1 -p 3
```
```bash
docker run -it --rm -v /run/desktop/mnt/host/wsl/PHYSICALDRIVE1p3/android/android_pie:/src android-build-trusty
```
```bash
cd /src; source build/envsetup.sh
```
```bash
lunch full_u7-userdebug
```
```bash
make -j8
```