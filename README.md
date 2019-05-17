# OPC UA Animal Server

OPC UA Server for the OPC UA Companion Specification for Animals - A Tutorial 

This repository shows how to use the OPC UA Animal companion specification from the repository:
https://github.com/Pro/opcua-animal-cs

The corresponding Tutorial can be found here:
https://opcua.rocks/custom-information-models/

## Build

First clone this repository and initialize the git submodule:

```bash
git clone https://github.com/Pro/opcua-animal-server
cd opcua-animal-server
git submodule update --init --recursive
```

Then just run CMake and make:

```bash
mkdir build
cd build
cmake ..
make -j
```

## Run

After building the repository, just run the executable:

```bash
cd build
./server_animal
```

Then use e.g. UaExpert to connect to the server.
The Endpoint URL is printed in the terminal, but should be the default: `opc.tcp://localhost:4840`

