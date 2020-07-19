# Illarion Coding Style

July 19, 2020

Author: Vilarion

Version 1.0

The team of Illarion developers has grown over time. And while everyone has their preferred coding
style, it is useful to agree on a single one. This makes it easier for others to read your code, understand
and modify it. These rules do not only cover the appearance of code, but also how the coding itself
is performed, which functionality to use or avoid and best practices. The purpose of this document
is not to hamper you in your coding efforts with an overly exhaustive set of rules, but to guide you
towards clean code for the benefit of all.

There are many languages involved in Illarion development. They range from mark-up languages
like HTML or the typesetting language LaTeX to a whole array of different programming languages
like C++ , Java, Lua, PHP or GLSL. Examples given, either conforming or non-conforming, will be
in C++ and Lua. You can easily derive how they would look like in the language you are currently
using. Rules are designed to be as general as possible to apply to most languages used in Illarion
development.

Examples are tagged with icons to annotate whether or not they are conforming. Non-conforming
examples are designed such, that only the current issue is being violated. They are correct in every
other aspect, so that you can focus on the issue at hand. This is what correct examples look like:

<table><tr><td></td><td>C++</td><td>Lua</td><tr><td>:heavy_check_mark:</td><td>

```cpp
for (auto &item: items) {
    item.age();
}
```
</td><td>

```lua
for _, item in pairs(items) do
    item.age()
end
```
</td></tr></table>

A violating example looks like this:

<table><tr><td></td><td>C++</td><td>Lua</td><tr><td>:x:</td><td>

```cpp
for (auto &item: items)
{
    item.age();
}
```
</td><td>

```lua
for _, item in pairs(items)
do
    item.age()
end
```
</td></tr></table>

##### Formatting

1. [Write lines not longer than 120 characters](#f-length)
2. [Write one statement per line](#f-one-statement)
3. [Frame code blocks with one line on each end](#f-frame)
4. [Seperate adjacent code blocks with an empty line](#f-blank-line)
5. [Indent four spaces inside code blocks](#f-space-indent)
6. [Use space after a delimiter](#f-space-delimeter)
7. [Use space before and after binary operators](#f-space-binary)
8. [Avoid space after function names](#f-space-function)
9. [Avoid trailing white space](#f-space-trailing)
10. [Use lowerCamelCase for variable and function names](#f-var-func-names)
11. [Use UpperCamelCase for class names](#f-class-names)
12. [Use proper British English](#f-language)
13. [Use block comments for license headers](#f-license)

##### Coding

1. [Select expressive names](#c-names)
2. [Write only useful comments](#c-comments)
3. [Avoid deprecated code](#c-deprecated)
4. [Avoid duplicating code](#c-duplicate)
5. [Use libraries](#c-libs)
6. [Keep it as local as possible](#c-local)
7. [Write short, expressive functions](#c-functions)
8. [Avoid unnecessary code and magic numbers](#c-magic)
9. [Refrain from using goto](#c-goto)
10. [Use correct license headers](#c-license)

## Formatting

<a name="f-length"></a>
### Write lines not longer than 120 characters

Long lines of code tend to get difficult to read. If your lines get longer than 120 characters, reconsider
what you are writing. In fact, most statements should fit into a line of 80 characters. Maybe there is
a better way to express what you want to do. If you still need longer lines, break them up, indenting
them further than the next statement.

This rule does not apply to continuous text e.g. in HTML. Breaking up continuous text can lead to
strange diffs where changing a single word could put a whole paragraph into the diff.

<a name="f-one-statement"></a>
### Write one statement per line

On the other hand, do not cram statements into one line until it reaches its length limit. One
statement per line allows for good readability. Compare:

<table><tr><td></td><td>C++</td><td>Lua</td><tr><td>:heavy_check_mark:</td><td>

```cpp
auto strength = 10;
auto wisdom = 8;
```
</td><td>

```lua
local strength = 10
local wisdom = 8
```
</td></tr><tr><td>:x:</td><td>

```cpp
auto strength = 10; auto wisdom = 8;
```
</td><td>

```lua
local strength = 10 local wisdom = 8
```
</td></tr></table>

<a name="f-frame"></a>
### Frame code blocks with one line on each end

Each local code block should be framed by one line on each end:

<table><tr><td></td><td>C++</td><td>Lua</td><tr><td>:heavy_check_mark:</td><td>

```cpp
for (auto &item: items) {
    item.age();
}
```
</td><td>

```lua
for _, item in pairs(items) do
    item.age()
end
```
</td></tr><tr><td>:x:</td><td>

```cpp
for (auto &item: items)
{
    item.age();
}
```
</td><td>

```lua
for _, item in pairs(items)
do
    item.age()
end
```
</td></tr></table>

<a name="f-blank-line"></a>
### Seperate adjacent code blocks with an empty line

You can also use an empty line to structure logical groups.

<table><tr><td></td><td>C++</td><td>Lua</td><tr><td>:heavy_check_mark:</td><td>

```cpp
auto minutes = 3;
auto seconds = minutes * 60;

for (auto &item: items) {
    for (auto i = 0; i < 5; ++i) {
        item.age(seconds);
    }
}
```
</td><td>

```lua
local minutes = 3
local seconds = minutes * 60

for _, item in pairs(items) do
    for i = 1, 5 do
        item.age(seconds)
    end
end
```
</td></tr><tr><td>:x:</td><td>

```cpp
auto minutes = 3;
auto seconds = minutes * 60;
for (auto &item: items) {

    for (auto i = 0; i < 5; ++i) {
        item.age(seconds);
    }
}
```
</td><td>

```lua
local minutes = 3

local seconds = minutes * 60
for _, item in pairs(items) do
    for i = 1, 5 do
        item.age(seconds)
    end
end
```
</td></tr></table>

<a name="f-space-indent"></a>
### Indent four spaces inside code blocks

Local code blocks have to be indented by four spaces. Do not use tabulators.

<table><tr><td></td><td>C++</td><td>Lua</td><tr><td>:heavy_check_mark:</td><td>

```cpp
{
    auto result = database.query();
    result.validate();
}
```
</td><td>

```lua
do
    local npc = getNPC()
    npc:talk("Hello!")
end
```
</td></tr><tr><td>:x:</td><td>

```cpp
{
        auto result = database.query();
        result.validate();
}
```
</td><td>

```lua
do
  local npc = getNPC()
  npc:talk("Hello!")
end
```
</td></tr></table>

<a name="f-space-delimeter"></a>
### Use space after a delimiter

Each delimiting character has to be followed by exactly one space:

<table><tr><td></td><td>C++</td><td>Lua</td><tr><td>:heavy_check_mark:</td><td>

```cpp
for (const auto number: {42, 0, 1}) {
    cout << number;
}
```
</td><td>

```lua
for number in {1, 2, 3} do
    print(number)
end
```
</td></tr><tr><td>:x:</td><td>

```cpp
for (const auto number:{42, 0, 1}) {
    cout << number;
}
```
</td><td>

```lua
for number in {1,2,3} do
    print(number)
end
```
</td></tr></table>

<a name="f-space-binary"></a>
### Use space before and after binary operators

All binary operators have to be pre- and succeeded by one space:

<table><tr><td></td><td>C++</td><td>Lua</td><tr><td>:heavy_check_mark:</td><td>

```cpp
cout << 1;
auto i = 0;
i += 2;
auto b = 3 * i;
```
</td><td>

```lua
print("a" .. "b")
local i = 0
i = i + 2
local b = 3 * i
```
</td></tr><tr><td>:x:</td><td>

```cpp
cout<<1;
auto i=0;
i +=2;
auto b =3*  i;
```
</td><td>

```lua
print("a".."b")
local i =0
i =i+ 2
local b= 3 * i
```
</td></tr></table>

<a name="f-space-function"></a>
### Avoid space after function names

This speaks for itself:

<table><tr><td></td><td>C++</td><td>Lua</td><tr><td>:heavy_check_mark:</td><td>

```cpp
std::move(object);
```
</td><td>

```lua
print(1)
```
</td></tr><tr><td>:x:</td><td>

```cpp
std::move (object);
```
</td><td>

```lua
print (1)
```
</td></tr></table>

<a name="f-space-trailing"></a>
### Avoid trailing white space

White space at the end of a line will produce strange diffs, so make sure you do not insert any.

<a name="f-var-func-names"></a>
### Use lowerCamelCase for variable and function names

Lower camel case means that the first letter of the first word is written in lower case while consecutive
words are directly appended but start with upper case:

<table><tr><td></td><td>C++</td><td>Lua</td><tr><td>:heavy_check_mark:</td><td>

```cpp
int playerCounter;
Player destroyerOfWorlds;
void fooBar();
```
</td><td>

```lua
local playerCounter
local robertOppenheimer

function fooBar()
end
```
</td></tr><tr><td>:x:</td><td>

```cpp
int playercounter;
Player destroyer_Of_Worlds;
void foo_bar();
```
</td><td>

```lua
local playercounter
local robert_Oppenheimer

function foo_bar()
end
```
</td></tr></table>

<a name="f-class-names"></a>
### Use UpperCamelCase for class names

Upper camel case means that a name consists of possibly multiple directly concatenated words, each
starting with a capital letter:

<table><tr><td></td><td>C++</td><td>Lua</td><tr><td>:heavy_check_mark:</td><td>

```cpp
class PlayerManager
struct Position;
class SelectionDialog;
```
</td><td>

```lua
PlayerCraft = {
    products = {},
    ...
}
```
</td></tr><tr><td>:x:</td><td>

```cpp
class playerManager
struct position;
class selection_dialog;
```
</td><td>

```lua
player_craft = {
    products = {},
    ...
}
```
</td></tr></table>

<a name="f-language"></a>
### Use proper British English

It is important to use proper language as well as the proper language. Others will have to read what
you write. Once we decided to use British English as official staff language, so this decision also
applies to all written code. Small mistakes might and will happen, but that is no excuse to be lazy
about it. Use a dictionary if you are not sure.

<a name="f-license"></a>
### Use block comments for license headers

Using block comments for license headers at the beginning of each file allows editors to fold them,
reducing the noise for you while you are working on actual code.

## Coding

<a name="c-names"></a>
### Select expressive names

Pick meaningful names. This is one of the most important aspects of good code. Do not use strange
abbreviations. Variable names should describe their content, not an underlying data structure or
implementation detail. Function names should describe an action for most functions and a question
for boolean functions:

<table><tr><td></td><td>C++</td><td>Lua</td><tr><td>:heavy_check_mark:</td><td>

```cpp
int playerCounter;
std::vector<Player> players;

for (auto i = 0; i < 10; ++i); // i is a common counter name

void savePlayers();
bool isYellow();
int getStrength();
```
</td><td>

```lua
local playerCounter

for i = 1, 10 do -- i is a common counter name
end

function useItem(user, item)
end
```
</td></tr><tr><td>:x:</td><td>

```cpp
int plCtr;
std::vector<Player> playerVector;
void f();
```
</td><td>

```lua
local plyCt

function calculate() -- calculate what?
end
```
</td></tr></table>

<a name="c-comments"></a>
### Write only useful comments

Express yourself in code instead of comments. Do not be redundant in comments. Do not use
comments to rant or be otherwise unprofessional. One example for a good comment would be the
description of a complex algorithm. You can cite the paper where you got it from and briefly express
what the algorithm does. Further examples would be documenting a function's precondition or a class' invariant.

<table><tr><td></td><td>C++</td><td>Lua</td><tr><td>:x:</td><td>

```cpp
int a = 0; // counts players
int playerCounter = 0; // set to 0

while (true) {
} // end while

int b = ++a + 2 - 3; // this code is shit!!!

// characterAge: the age of the characters
// returns the number of characters
int numberOfCharacters(int characterAge);
```
</td><td>

```lua
local agility = 0 -- holds agility
local attribute = agility or 0 -- set attribute to agility or 0 if agility is nil

-- begin setting attributes
agility = 5
-- end setting attributes
```
</td></tr></table>

<a name="c-deprecated"></a>
### Avoid deprecated code

Deprecated code will create work when we decide to use a newer version of some language. Do not use
it, there is no excuse. Others will have to replace that code in time. If you come across deprecated
code, get rid of it.

You should be aware of what is marked as deprecated in the language version you are currently
using.

<table><tr><td></td><td>C++</td><td>Lua</td><tr><td>:heavy_check_mark:</td><td>

```cpp
std::unique_ptr<Network>;
void save() noexcept;
~Player();
```
</td><td>

```lua
local M = {}
...
return M

length = #{4, 3, 2}
log = math.log(1234, 10)
```
</td></tr><tr><td>:x:</td><td>

```cpp
std::auto_ptr<Network>;
void save() throw();
~Player() throw();
```
</td><td>

```lua
module("base.common", package.seeall)

length = table.maxn{4, 3, 2}
log = math.log10(1234)
```
</td></tr></table>

<a name="c-duplicate"></a>
### Avoid duplicating code

Do not duplicate code. Copy&paste is bad. You or someone else will change that code in one place
later and forget the other occurrences or not even know about them. Use functions if you need a
piece of code more than once. Also use functions to clarify. If you can name it, you can put it into a
function.

<a name="c-libs"></a>
### Use libraries

Prefer using language features or language libraries over reinventing the wheel. There is a reason
those things exist. Your own code will just be inefficient, more verbose and may even contain bugs.

<a name="c-local"></a>
### Keep it as local as possible

Keep the scope of variables as narrow as possible. The shorter their life span is, the less error-prone
is your design.

<a name="c-functions"></a>
### Write short, expressive functions

Functions should be short and do one thing, specified by their name. If they are long and do things
they are not supposed to do, it gets difficult to understand them or reason about them.

<a name="c-magic"></a>
### Avoid unnecessary code and magic numbers

Be precise in what you write. Write enough so that the code is clear and meaningful, but do not be
verbose. Sometimes it is not enought to give a magic number a name, but you might need to change its type as well
to better reflect its content.

<table><tr><td></td><td>C++</td><td>Lua</td><tr><td>:heavy_check_mark:</td><td>

```cpp
auto taskInterval = std::chrono::seconds(60);
addUnsignedCharToBuffer(((data >> CHAR_BIT) & UCHAR_MAX));
return player;
```
</td><td>

```lua
activePlayers = 0
local strength = getAttribute(Character.strength)

if attribute == Character.dexterity then
    ...
end

do
    ...
end
```
</td></tr><tr><td>:x:</td><td>

```cpp
int taskInterval = 60; -- 60 what?
addUnsignedCharToBuffer(((data >> 8) & 255));
return (player);
```
</td><td>

```lua
a = 0; -- the ; is unnecessary in Lua, don't use it
i = (a * 3) + 2
local strength = getAttribute(5)

if (i == 4) then
    ...
end

if true
    ...
end
```
</td></tr></table>

<a name="c-goto"></a>
### Refrain from using goto

A form of the goto control statement exists in most languages. Do not use it.

<a name="c-license"></a>
### Use correct license headers

Every user-written source file which runs on the server needs to be prefixed with the AGPLv3 header.
This is true for everything we write in C++, Lua or PHP. Everything which will eventually run on a
client machine needs to be prefixed with the GPLv3 header.
