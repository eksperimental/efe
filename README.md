# Elixir Flavoured Erlang

An Erlang to Elixir Transpiler

An escript

## Build

```sh
rebar3 escriptize
```

## Run

The general format is:

```sh
efe pp file.conf file.erl+
```

where `file.conf` is a config file with the following format:

```erl
#{
   % blobs, if relative (start with .) are joined with current erlang file directory
   includes => [".", "../../*/include", "../../*/src"],
   % map of macro names and what they should expand to
   macros => #{'VSN' => '1.0', 'COMPILER_VSN' => '2.0'},
   encoding => latin1, % or utf8
   output_dir => "./out",
   % prefix to add to compiled modules, useful when transpiling otp to avoid
   % conflicts
   mod_prefix => "m_"
}.
```

Here is the config used to transpile [cowboy](https://github.com/ninenines/cowboy/)

```erl
#{
   includes => [".", "../include", "../../"],
   macros => #{},
   encoding => utf8,
   output_dir => "./out"
}.
```

### Transpiling OTP

```
git clone git@github.com:erlang/otp.git
mkdir -p out
./efe pp otp.conf otp/lib/*/src/*.erl otp/erts/preloaded/src/.erl

```

Results in out/otp/

### Transpiling Cowboy

```sh
git clone https://github.com/ninenines/cowboy.git
# need header files from cowlib
git clone https://github.com/ninenines/cowlib.git
mkdir -p out
./efe pp cowboy.conf cowboy/src/*.erl
```

Results in out/cowboy
