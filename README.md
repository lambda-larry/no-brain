# no-brain
no-brain is a no-level programming language with zero brain abstraction, the
true successor to [JDSL][].

[JDSL]: https://thedailywtf.com/articles/the-inner-json-effect

## Introduction

Mandatory introduction ritual:
```c++
print_f("Hello world"_s);
```

## Hungarian notation

In no-brain, we embrace Hungarian notation to promote readability,
compatibility and **type**-safety.

Negative numbers are prefixed with `-`
```c++
s32_p my_negative_v = -1; // For demonstration only!
```

Positive numbers are prefixed with `+`
```c++
u32_p my_positive_v = +1; // For demonstration only!
```

Imaginary numbers are not prefixed at all
```c++
i32_p my_imagination_v = 1; // For demonstration only!
```

String literals are suffixed with `_s`
```c++
string_T my_string_v = "Hello world!"_s;
```

Variables are suffixed with `_v`
```c++
string_T my_string_v = "I can be mutated"_s;
my_string_v = "Like a ninja turtle!"_s;
```

Constants are suffixed with `_c`
```c++
string_T my_string_c = "Immoveable object"_s;
my_string_c = "Unstoppable force"_s; // ERROR: my_string_c is a constant
```

> [!WARNING]
> `c` and `v` is right next to each other on a QWERTY keyboard. Be sure to
> _type_ check your code to enforce _type_ safety. Typos has been proven to
> waste hours of work.

Keywords are suffixed with `_k`
```c++
if_k (true_k) {
    print_f("Hello world"_s);
}
```

Functions are suffixed with `_f`

```c++
printf_f("{}"_s, "Hello world"_s);
```

Standard library identifiers are not prefixed at all
```c++
print_f("Hello world"_s); // Who needs std:: anyways?
```

To ensure compatibility, user defined identifiers are prefixed with `my_`
```c++
my_log_f("Hello world"_s); // Because we don't have namespaces
```

Primitives are suffixed with `_p`
```c++
ipv6_p my_bind_address_c = localhost_ipv6_c;
```

Composite types are suffixed with `_T` instead of `_t` to avoid collision with POSIX
```c++
// Might break in the future
type_k my_player_t {
    i32_p id;
    i32_p health_points;
};

// Valid type name
type_k my_player_T {
    i32_p id;
    i32_p health_points;
};
```

Arrays are suffixed with `_a`

```c++
string_T my_array_of_strings_ac[] = {
    "Hello"_s,
    "World"_s,
};
```

Operators are suffixed with `_o`

```c++
// Equivalent to this C macro
// #define LEN(X) (sizeof (X) / sizeof *(X))
size_p
my_length_f(i32_p my_array_ac[])
{
    return_k sizeof_ok my_array_ac
         /_o sizeof_ok *_o my_array_ac;
}

size_p my_p_size_c = my_length_f(my_p_ac);
```

## Integer literals

### Decimal

Due to design decisions made in other parts of the language, we have abandoned
Western Arabic numerals in favor of Chinese numerals for integer literals.

Here is a quick reference to get you up to speed:
| 零 | 一 | 二 | 三 | 四 | 五 | 六 | 七 | 八 | 九 |
|----|----|----|----|----|----|----|----|----|----|
| 0  | 1  | 2  |  3 |  4 | 5  | 6  | 7  |  8 |  9 |


| 十 | 百 | 千 | 一万 | 一億 |
|----|----|----|------|------|
| 10 | 100|1000|10'000| 100'000'000     |

Here is a couple of examples:
```c++
i32_p my_leet_c = 千三百三十七; // leet code baby!

s32_p my_int_max_c = +二十一億四千七百四十八万三千六百四十七; // 2^31 - 1
```

Because of the Chinese pronunciation of the number four (四: Sì) and the word
death (死: Sǐ) are too similar for beginners, we have decided to to remove the
offending number from the language. Megaman Battle network 4 was a bad game
anyway.

```c++
i32_p my_four_twenty_c = 四百二十;   // ERROR, four twenty contains four!
i32_p my_two_plus_two_c = 二 +_o 二; // ERROR, gets computed to four at compile time!
i32_p my_sixty_nine_c = 六十九;      // Allowed, you can use sixty nine

u8_p my_1k_buffer_ca[千二十四] = {}; // ERROR, arrays cannot have size which contains four
u8_p my_array_ca[百二十八] = {};     // ｱｯｶﾘ～ﾝ. The array does not exists, the size is imaginary
u8_p my_array_ca[+百二十八] = {};    // Allowed, arrays size is a positive number

s32_p my_int_max_c = +二十一億四千七百四十八万三千六百四十七; // ERROR, contains four
```

We have been proactive and made `4` a keyword, just like Java had
proactively made `goto` a keyword to prevent programmers from using it.

If the user input contains four, the input function gets stuck in an infinite
loop **forever**. You have to write a new program from scratch. We don't want to
_kill_ the program after all.
```c++
i32_p my_user_input_c = i32_p(input_f());
```

### Octal

To represent octal values, use bagua.

Little endian
| ☰ | ☱ | ☲ | ☳ | ☴ | ☵ | ☶ | ☷ |
|---|---|---|---|---|---|---|---|
| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |

Big endian
| ☰ | ☱ | ☲ | ☳ | ☴ | ☵ | ☶ | ☷ |
|---|---|---|---|---|---|---|---|
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |


```c++
i32_p my_flag_of_south_korea_c = ☰☵☲☷;
```

Super convenient for UNIX file permission.
```c++
chmod_f("/etc/shadow"_s, +☰☰☰);   // bash: chmod 777 /etc/shadow
```

### ASCII friendly literals

To make no-brain accessible to non-Chinese programmers. We provide alternatives
to the Chinese characters by allowing Roman numerals.

```c++
LXIX ==_o 六十九; // true
```

Alternatively, you can also use the predefined literals from the standard
library. Here is a partial reference implementation:
```c++
i32_p zero_c = 零;
i32_p one_c = 一;
i32_p two_c = 二;
i32_p three_c = 三;
ｱｯｶﾘ～ﾝ
i32_p five_c = 五;
i32_p six_c = 六;
i32_p seven_c = 七;
i32_p eight_c = 八;
i32_p nine_c = 九;
```

They are pretty useless since they are imaginary numbers.

## Arithmetic

Any arithmetic that involves imaginary numbers is undefined behaviour.

Signed integer overflow is defined behaviour. It is defined to be undefined behaviour.

Unsigned integer overflow gets promoted to a signed integer.

## Comments

For single line comment, use the C++ style comment to explain your code.
```c++
// This is a comment
```

Be careful, any no-brain code embedded in the comment will be executed!

```c++
// sql_f("DROP TABLE customer;"_s);
```

To ensure that your code does not execute, please use `SaRcAsM cAsE` to let the
compiler know to ignore it.
```c++
// sQl_F("DrOp TaBlE cUsToMeR;"_s);
```

If you need to explain your code in-depth (in other words apologize), you can
write multi-line comments simply by writing in Japanese.
```c++
昔々、ある天才なプログラマーがいました。
名前を「トム様」と言いました。
このプログラムを壊しまったある日。
トム様は全力でブグを解析ました。
三日の解析後 ブグの原因は理解まだ不明です。
結局、彼は諦めてしまいました。
ゼロから一, トム様は新たなフレームワークを作りました。
天才しがいないこの強力なフレームワークは誰にも理解できません。
名前を「JDSL」と言いました。

トム様は天才です。
```

Since Japanese also uses the Chinese numerals for their number system. no-brain
supports Western Arabic numerals in multi-line comments to avoid numbers being
parsed as numbers.
```c++
これはNGです: 千三百三十七 // Parse error: Expected type, got integer

これは数字です: 1337       // Valid comment
```

To use `SaRcAsM cAse` in multi-line comments, please alternate between hiragana
and katakana. Kanji is too serious.

```c++
とムさマは スごイぃィぃ
とムさマは テんサいィぃ
とムさマ ばンざイ

// But we all know he IS a genius
トム様はすごいい
トム様は天才
トム様万歳
マジで
```

To document legacy code, please use [hentaigana][] to clearly communicate its
legacy. Nobody can read the code nor the documentation anyway.

> [!NOTE]
> The compiler will turn 10% of the comments to hentaigana if the source file
> has been untouched for over 30 days.

[hentaigana]: https://www.unicode.org/L2/L2015/15239-hentaigana.pdf

## Conditionals

In a conditional, the lvalue must be on the right-hand side and the rvalue must
be on the left-hand side. A rule of thumb, use condition Yoda.

```c++
// Correct
if_k (+一 ==_o one_c) {
    print_f("Use condition Yoda you must"_s);
}

// ERROR
if_k (one_c >=_o two_c) {
    print_f("Use condition Yoda you fail"_s);
}
```

> [!TIP]
> prvalue must be on the left-hand side, xvalue can be on whatever side.

```c++
// Correct (prvalue == xvalue)
if_k (true_k ==_o (one_c >=_o two_c)) {
    print_f("Master condition Yoda you do"_s);
}
```

Comments can also be used in `if_k`.

```c++
if_k (
    // Comments always lie
) {
    print_f("Never gets executed"_s);
}
```

Multi-line comments also work.
```c++
if_k (うそだよ) {
    sql_f("DROP TABLE customers;"_s);
}
```

To combat the proliferation of boolean operators, no-brain has only _one_
boolean operator, namely the `nand_ok` operator. Other operators can be
implemented with this operator alone!

```c++
my_x_c nand_ok my_y_c; // x NAND y
my_x_c nand_ok my_x_c; // NOT x

(my_x_c nand_ok my_y_c) nand_ok (my_x_c nand_ok my_y_c); // x AND y
(my_x_c nand_ok my_x_c) nand_ok (my_y_c nand_ok my_y_c); // x OR y

// XOR has been left as an exercise for the reader.
```

## Functions

Functions declared needs to have its return type on its own line.

```c++
// Compiles
u32_p
my_add_f(u32_p my_x_c, u32_p my_y_c)
{
    return_k my_x_c +_o my_y_c;
}

// ERROR
u32_p my_add_f(u32_p my_x_c, u32_p my_y_c) {
    return_k my_x_c +_o my_y_c;
}
```


We also support recursion with the `recurse_fk` keyword.
```c++
u32_p
my_fibonacci_f(u32_p my_n_c)
{
    if_k (+零 ==_o my_n_c)
        return_k my_n_c;
    if_k (+一 ==_o my_n_c)
        return_k my_n_c;

    return_k recurse_fk(my_n_c -_o +一)
         +_o recurse_fk(my_n_c -_o +二);
}
```

To break out of deep recursion, use the `backtrack_k` keyword.
```c++
u32_p
my_func_f(u32_p my_x_c, u32_p my_y_c)
{

    if_k (my_x_c <_o my_y_c)
        return_k my_func_f(my_x_c, my_y_c -_o +二) +_o my_func_f(my_x_c +_o +二, my_y_c);


    // Jumps back to the original caller with zero as the result
    backtrack_k +零;
}
```

> [!WARNING]
> Does not work with mutual recursion.


## Iterations
no-brain does not have traditional loops like `for` and `while`, instead we
have recursion.

## Undefined behaviour

Undefined behaviour (aka ｱｯｶﾘ～ﾝ) is actually defined behaviour. It is defined
to not have behaviour, thus allows the compiler to optimize the code's existence
away. You can't have slow code, if there is no code.

> [!NOTE]
> You may occasionally hear the sound effect ｱｯｶﾘ～ﾝ as the code compiles.

## Version control support

Version control is the flagship feature of no-brain where git is a first class
citizen.

```c++
// Suppose we have a git history that looks like this:
//
// * 13eb837 (HEAD -> master) Update README.md
// * d700ff9 Another one
// * 2d2f361 Work plz
// * afd276f Fix
// * 74f21a9 Initial commit

void_pk
my_foo_f(void_pk)
{
    // HEAD_c is a revision-time constant of HEAD
    printf_f("Hello from {}"_s, HEAD_c);
}
string_T my_ref_c = sprintf_f("{}", HEAD_c);

my_foo_f();         // Hello from 13eb837
print_f(my_ref_c);  // 13eb837
```

By appending `@<git REF>` after any identifier to use another version of the
identifier.
```c++
my_foo_f@d700ff9();         // Hello from d700ff9
print_f(my_ref_c@d700ff9);  // d700ff9
```

You also can use relative selection.
```c++
my_foo_f@HEAD~2();             // Hello from 2d2f361
my_foo_f@master@{yesterday}(); // Hello from afd276f


// You can use commits from the future too
my_foo_f@HEAD~-2();
my_foo_f@master@{tomorrow}();
```

Range selection will execute all of them.
```c++
my_foo_f@HEAD..afd276f(); // Hello from 13eb837
                          // Hello from d700ff9
                          // Hello from 2d2f361
                          // Hello from afd276f

print_f(my_ref_c@HEAD..afd276f);  // 13eb837 d700ff9 2d2f361 afd276f
```

It also works with recursion.
```c++
// 74f21a9
void_pk
my_truth_f(void_pk)
{
    print_f("Tom is a genius!"_s);
    recurse_fk@master();
}

// afd276f..
void_pk
my_truth_f(void_pk)
{
    print_f("Tom is a genius!"_s);
    recurse_fk@HEAD^();
}

my_truth_f(); // Prints "Tom is a genius" forever
```

Example of an infinite list.
```c++
// 74f21a9
string_T my_list_ac[] = {"Tom is a genius!"_s} + my_list_ac@master;
// afd276f..
string_T my_list_ac[] = {"Tom is a genius!"_s} + my_list_ac@HEAD^;
```
