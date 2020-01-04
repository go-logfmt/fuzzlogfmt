# fuzzlogfmt

Package fuzzlogfmt implements fuzzing functions compatible with
github.com/dvyukov/go-gofuzz to test github.com/go-logfmt/logfmt.

## Fuzzing functions

`func Fuzz` tests that any input accepted by `logfmt.Decoder` can be written by
`logfmt.Encoder` and that a second round trip of the data produces identical
output.

`func FuzzVsKR` tests that any input accepted by `logfmt.Decoder` is also
accepted by `github.com/kr/logfmt.Unmarshal`.

## Usage

### Installing go-fuzz

The installation instructions for go-fuzz are a bit buried in that project's
README. For convenience the command is:

```
go get -u github.com/dvyukov/go-fuzz/go-fuzz github.com/dvyukov/go-fuzz/go-fuzz-build
```

### Building the fuzzing binary:

After cloning this repository and changing dir to its root dir run

```
go-fuzz-build
```

That should produce a file name `fuzzlogfmt-fuzz.zip`.

### Fuzzing commands

To fuzz with `func Fuzz` run the following command.

```
go-fuzz -bin=fuzzlogfmt-fuzz.zip -func=Fuzz -workdir=_testdata
```

To fuzz with `func FuzzVsKR` run the following command.

```
go-fuzz -bin=fuzzlogfmt-fuzz.zip -func=FuzzVsKR -workdir=_testdata_vskr
```
