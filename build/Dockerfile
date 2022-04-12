FROM ubuntu AS builder
ENV DEBIAN_FRONTEND=noninteractive

RUN apt update -y 
RUN apt -y install curl git gcc pkg-config

RUN curl https://sh.rustup.rs -sSf | sh -s -- -y 
ENV PATH $PATH:$HOME/.cargo/bin

RUN git clone https://github.com/solana-labs/solana.git

WORKDIR /solana
RUN apt install -y libudev-dev
RUN apt install -y clang-9 clang-tools-9 clang-tidy-9 clang-format-9 lldb-9 lld-9 
RUN apt install -y libsecp256k1-dev
RUN apt install -y make g++ cmake libssl-dev
RUN . /root/.cargo/env && ./scripts/cargo-install-all.sh .

FROM ubuntu 
COPY --from=builder /solana/bin /solana/bin
ENV PATH /solana/bin:$PATH

