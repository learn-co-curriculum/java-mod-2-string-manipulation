# String Manipulation

## Learning Goals

- Discuss the `String` class
- Introduce the String Pool and new String objects
- Discuss some of the `String` class' methods

## Introduction

The `String` data type is one of the first data types we started using! But up
until now, we haven't really talked about the `String` class itself. We already
know that it is an immutable reference type and can be made up of a sequence of
characters, but can it do more?

## The `String` class

**The `String` class** has multiple methods for analyzing the contents of
strings, finding characters, locating substrings, changing the case, and so much
more! When we start performing these types of methods on `String` data types,
we typically refer to this as **string manipulation** as we are manipulating the
`String`.

We saw in the last lesson a couple of methods that belong to the `String` class,
the like constructor that takes a character array and the `toCharArray()`
method used to convert a `String` into a `char[]`.

Let's look closer at the constructors for the `String` class.

## Constructing Strings

As we have seen in previous lessons, we can initialize a `String` like this:

```java
String cat = "Tom";
```

This way used a **string literal** to assign a value to a `String` data type.
When we assign a string literal to a `String`, what Java does is it looks for
any other `String` variable assigned to that value in a special place in
memory called a **string pool**. If it does not find another `String` object in
the string pool with that value, then it will create the object. But if it
_does_ find another `String` with that value, Java will return a reference to
its memory address and not create another object.

![String Pool with Literals](https://curriculum-content.s3.amazonaws.com/java-mod-2/string-manipulation/String-Pool-Literal.png)

Now what if we want to have two different `String` objects with the same value?
Java's `String` class actually comes with constructors, so we can use the `new`
keyword to help instantiate the `String` variable!

```java
public class StringCatExample {
    public static void main(String[] args) {
        char[] charArray = {'T', 'o', 'm', '-', 'C', 'a', 't'};
        String name = "Tom-Cat";
        String cat1 = new String();
        String cat2 = new String(name);
        String cat3 = new String(charArray);
        String cat4 = new String(charArray, 0, 3);
    }
}
```

By using the constructors, we are instantiating the `String` variables and
forcing Java to create new objects and store them in the heap space instead of
the string pool.

![String Pool with Literals and Heap](https://curriculum-content.s3.amazonaws.com/java-mod-2/string-manipulation/String-Pool-with-Objects.png)


To better explain some of these constructors, let's look at each one:

1. The first constructor does not take any parameters - this will instantiate
   the `String` variable `cat1` to an empty string; which we can show with two
   double quotes with nothing inside them: `""`.
2. The second constructor takes in a `String` as a parameter. This will
   instantiate the `String` variable to the value of the `String` we pass in.
   So in this case, it will instantiate the `cat2` to "Tom-Cat".
3. The third constructor takes in a character array as an argument and will
   convert the contents of the character array to a `String` as we saw in the
   previous lesson. In this case, `cat3` will be assigned "Tom-Cat" as well.
   Notice that even though `cat2` and `cat3` have the same value, we still
   create a new `String` object since we are explicitly using the `new`
   keyword.
4. The fourth constructor takes in 3 arguments: a character array, an integer
   to represent the offset, and another integer to represent the count. What
   this will do is it will take the character array and convert only part of it
   to a `String` object. The part it will create is defined by the offset and
   the count. The offset is the index of the array we want to start creating the
   `String` object at and the count is how many characters we expect to be in
   the object. In this case, we start the offset at the 0 index, so 'T', and we
   are expecting there to be 3 characters in the object. So we count the `char`
   values and assign `cat4` to "Tom". If the offset had started at 4 instead,
   then the value of `cat4` would be "Cat" instead of "Tom".

## `String` methods

The `String` class also contains several useful methods for us to manipulate
`String` objects as well! We will review the more important methods within the
rest of this lesson and the next lesson.

### Length

Similar to how we can find the length of an array, we can find the length of a
`String`! To find the length of a `String`, we can call the `String` class'
`length()` method:

```java
public class StringExample {
    public static void main(String[] args) {
       String greeting = "Hello World";
       System.out.println("The length of the greeting is " + greeting.length());       
    }
}
```

The above will output:

```plaintext
The length of the greeting is 11
```

### Concatenating Strings

In the previous module, we saw how we could combine two string values using the
`+` operator:

```java
String string1 = "Tom";
String string2 = "Cat";

String result = string1 + string2;
```

When we use the `+` with `string1` and `string2`, we would evaluate the
expression to "TomCat" and assign that value to the `result` variable. This is
an example of **concatenating strings**, which is how we can combine multiple
`String` values together.

There is another way we could concatenate strings and that is using the method
`concat()` from the `String` class! The `concat()` method takes in one
parameter, a `String`, and combines it with the calling `String` object.

```java
String string1 = "Tom";
String string2 = "Cat";

String result = string1.concat(string2);
```

When the `concat()` method is called, it will take the `string2` value and
concatenate it with the `string1` value by appending `string2` at the end of
`string1`. Therefore, the `result` would be "TomCat" -- the same output we saw
when we combine `String` objects using the `+` operator! It should be noted that
`string1` and `string2` do not change values when using the `concat()` method.

### Changing the Case

We may want to change the casing of a `String` object to all lowercase or all
uppercase characters sometimes. Luckily, the `String` class has two methods
that can help us out with this! These two methods are called `toUpperCase()` and
`toLowerCase()`. Both of these methods will return a `String` value of the
original `String` but with all the characters changed to specified case.

```java
public class StringCatExample {
    public static void main(String[] args) {
        String original = "TomCat";
        String uppercase = original.toUpperCase();
        String lowercase = original.toLowerCase();
        
        System.out.println(uppercase);
        System.out.println(lowercase);
    }
}
```

When we execute the code above, we will end up with a result like this:

```plaintext
TOMCAT
tomcat
```

### Indexes and Characters

Since Java defines a `String` as a single unit of a sequence of characters, we
can look at `String` objects as having indexes like we do with character arrays.
For example, if we look at the `String` "Cat", in Java, the 'C' would be at
index 0, the 'a' would be at index 1, and the 't' would be at index 2. Knowing
this will help us manipulate our `String` objects more efficiently. There is
even a `charAt()` method to help us get a character at a specific index within
a `String`:

```java
public class StringCatExample {
    public static void main(String[] args) {
       String cat = "Cat";
       char character = cat.charAt(1);
       
       System.out.println(character);
    }
}
```

The following output of this would be:

```plaintext
a
```

### Contains and Substrings

Consider this: We want to know if a `String` contains a specific sequence of
characters. Maybe we are looking for the word `cat` within a string. We can
confirm if the sequence of characters is contained within a `String` by calling
the `contains()` method. The `contains()` method returns a boolean value - so if
the sequence is found, it will return true, else it will return false.

```java
String greeting = "Helo World";

if (greeting.contains("cat")) {
    System.out.println("We found the cat!");
} else {
    System.out.println("I guess we need to keep looking!");
}
```

In the example above, we can check to see if the `String greeting` contains the
value of `cat` by calling the `contains()` method. The character sequence of
interest will be passed as a parameter to the `contains()` method and will
search the original `String` object, `greeting` to see if the sequence is found
within the value. In this case, `cat` is not contained within `greeting`, so
the `contains()` method will return false.

When looking for a specific sequence of characters within a `String`, we tend
to call the bit we are looking for a **substring**. A substring is part of a
`String` value. For example, a substring of the word "tomcat" is "tom". The
substring does not necessarily have to be an English word either. "mc" is just
as much of a substring of "tomcat" as "tom".

The `String` class has two methods to get a substring that will each create a
new `String` object by copying part of an existing `String`:

```java
String greeting "Hello World";
String substring1 = greeting.substring(6);
String substring2 = greeting.substring(0, 5);
```

![String with Indices](https://curriculum-content.s3.amazonaws.com/java-mod-2/string-manipulation/String-Index.png)

Let's look a little closer at these two different `substring()` methods:

- The first `substring()` method only takes in one parameter, the starting index
  of the original `String`, `greeting`. It will then return the substring of the
  original `String` beginning at the index given. So in this example,
  `greeting.substring(6)` would evaluate to "World".
- The second `substring()` method takes in two parameters, a starting index and
  the ending index of the original `String`. This method returns a substring of
  the original `String` starting at the starting index and ending at the
  ending index. It should be noted that the ending index is **not** inclusive,
  so `greeting.substring(0,5)` will return only "Hello" and not the space after
  it.

### Replacing Characters

Sometimes we might want to perform something like a "find and replace" within
our `String` object. For example, maybe we have a want to replace "Tom" with
the word "Garfield" in a string of words. Can the `String` class help with this?

The answer is yes! The `String` class has a method called `replace()` that will
take two parameters: the sequence of characters we want to replace, and new the
sequence of characters we'd like to replace it with. The `replace()` method will
also return a new `String` object with the replaced characters.

```java
String string1 = "Tom the cat";

String string2 = original.replace("Tom", "Garfield");
```

The above code will take the original `String`, `string1` and replace all
occurrences of "Tom" with "Garfield". This will return a new `String` with the
value "Garfield the cat". Note that the original `string1` does not change.
