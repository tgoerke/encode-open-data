# Encode Open Data Hackathon

This project demonstrates how to run a WASM container as a bacalhau job. 


## Prepare for the hackathon


````
# Install lilipad and bacalhau CLI and do some tests
curl -sSL -O https://raw.githubusercontent.com/bacalhau-project/lilypad-modicum/main/lilypad && sudo install lilypad /usr/local/bin/lilypad
lilypad
export PRIVATE_KEY=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
lilypad run cowsay:v0.0.1 "hello lilypad"
ipfs get QmNjJUyFZpSg7HC9akujZ6KHWvJbCEytre3NRSMHzCA6NR
lilypad run fastchat:v0.0.1 QmcPjQwVcJiFge3yNjVL2NoZsTQ3GBpXAZe21S2Ncg16Gt
curl -sL https://get.bacalhau.org/install.sh | bash
mkdir encode-open-data
cd encode-open-data/
````
# Install WASM dev tools
````
curl https://get.wasmer.io -sSfL | sh
curl https://raw.githubusercontent.com/wasienv/wasienv/master/install.sh | sh
source $HOME/.wasienv/wasienv.sh
curl https://wasmtime.dev/install.sh -sSf | bash
export WASMTIME_HOME="$HOME/.wasmtime"
````

## Compile as WASM

WebAssembly (or Wasm) is an exciting technology for deploying highly secure, performant, and portable code
allowing developers to deploy applications transparently across multiple architectures and without any rewrites from languages like Rust, C, and C++.
A good resource to get started is wasm.builders

For this project we will compile Rust code to create the Sierpinsky triangle as ASCII art for your terminal :)

````
# https://www.rosettacode.org/wiki/Sierpinski_triangle#Rust
cargo new hello-rust
cat >sierpinski.rs
mv sierpinski.rs hello-rust/src/main.rs
cd  hello-rust
cargo build
cargo run
cargo build --target wasm32-wasi --release
# Run locally
wasmtime target/wasm32-wasi/release/hello-rust.wasm
````
## Submit to Bacalhau network

Bacalhau is language-agnostic, and supports Docker or WASM workloads. As long as you can run your executable in a container, you can run it in Bacalhau.

````
bacalhau wasm run  target/wasm32-wasi/release/hello-rust.wasm 
````
## Get results
````
bacalhau get 286430e2-9011-4796-bf4b-98be5022399b
less job-286430e2/stdout 
bacalhau describe --json 286430e2-9011-4796-bf4b-98be5022399b >sierpinski.json
jq . <sierpinski.json |less
````


## Resources

- https://www.wasm.builders/kirteeprajapati/rust-with-webassembly-2415
- https://www.rosettacode.org/wiki/Sierpinski_triangle#Rust
- https://docs.bacalhau.org/getting-started/wasm-workload-onboarding/
- https://docs.bacalhau.org/examples/workload-onboarding/rust-wasm/
- https://docs.lilypadnetwork.org/lilypad-v0-reference/creating-your-own-jobs


cat >Pascal.cpp
g++ Pascal.cpp -o Pascal
./Pascal 
echo 5|./Pascal 
wasic++ Pascal.cpp -o Pascal.wasm
cat /home/torsten/.bashrc
g++ Pascal.cpp -o Pascal
wasic++ Pascal.cpp -o Pascal.wasm
cargo new hello-rust
cd hello-rust/
vi src/main.rs 
cargo build --target=wasm32-wasi --release
wasmtime target/wasm32-wasi/release/hello-rust.wasm

git clone https://github.com/danmack/sierpinski-rs.git
cd sierpinski-rs/
ls
cargo build
cargo run
ls
xdg-open tri.png 
cargo build --target=wasm32-was --release
cargo build --target=wasm32-wasi --release
ls
wasmtime target/wasm32-wasi/release/triangle.wasm 
cargo build --target=wasm32-wasi --release
cargo run
cp target/wasm32-wasi/release/triangle.wasm  .
wasmtime triangle.wasm 
bacalhau wasm validate triangle.wasm 
bacalhau wasm run triangle.wasm 
wasmtime triangle.wasm 
cargo build --target=wasm32-wasi 
wasmtime target/wasm32-wasi/release/triangle.wasm 
cd ..

git clone https://github.com/lerina/wasm-Sierpi-ski.git
cd wasm-Sierpi-ski/
cargo build
cargo run
./run.sh 
less src/lib.rs 
cd ..


