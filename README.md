# dockerfiles

This project includes various docker images for the shift-left testing project.


## How to build docker images

### ubuntu-dev

    $ docker build -f ubuntu-dev/Dockerfile -t ubuntu-dev .

### yocto-dev

    $ docker build -f yocto-dev/18.04/Dockerfile -t yocto-dev-18.04 .
    $ docker build -f yocto-dev/16.04/Dockerfile -t yocto-dev-16.04 .

### jenkins-dev

    $ docker build -f jenkins-dev/Dockerfile -t jenkins-dev .

### clang-dev

    $ docker build -f clang-dev/11/Dockerfile -t clang-dev-11 .
    $ docker build -f clang-dev/10/Dockerfile -t clang-dev-10 .
    $ docker build -f clang-dev/9/Dockerfile -t clang-dev-9 .


## Licenses

This project source code is available under MIT license. See [LICENSE](LICENSE).
