# llvm-studies
Notes and snippets from my explorations of using LLVM IR as a universal assembly language.

## Installation on macOS

Brew works!
```bash
brew install llvm
```
That's a lot of `l`s! Since a version of llvm ships with macOS, brew won't add the llvm bin-directory `/usr/local/opt/llvm/bin` to your path, you can do so manually.

## Testing LLVM IR
We can use the following program `test.ll` to test-drive our installation:
```
define i32 @sum(i32 %a, i32 %b) {
  %sum = add i32 %a, %b
  ret i32 %sum
}

define i32 @main() {
  %a = add i32 1, 0
  %b = add i32 2, 0
  %c = add i32 3, 0
  %ab = call i32 @sum(i32 %a, i32 %b)
  %abc = call i32 @sum(i32 %ab, i32 %c)
  ret i32 %abc
}
```
'Compile' and run it using:
```bash
llc -o test.S test.ll
gcc -o test test.S
./test
echo $?
```
