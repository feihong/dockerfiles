# CentOS 7 with Elixir installed

This is for building production releases that can run on WebFaction.

Source: https://gist.github.com/binarytemple-clients/52bec05fc9bdba80d737

## Build

    docker build -t centos-7-elixir .

## Run

    docker run -it centos-7-elixir

## Compile for release

    docker run -it --mount type=bind,source=`pwd`,target=/src centos-7-elixir \
      ENV=prod mix release --env=prod

## Links

- [Elixir Releases](https://github.com/elixir-lang/elixir/releases)
- [How to Install Erlang and Elixir on CentOS 7](https://myvpsource.com/install-erlang-elixir-centos-7)
- [Please ensure your locale is set to UTF-8](https://github.com/elixir-lang/elixir/issues/3548)
