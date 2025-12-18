---
title: Using Operators in Your Programs
aliases:
  - Java Operators
  - Using Operators in Your Programs
categories:
  - "[[Posts]]"
tags:
  - Java
  - Operators
  - Programming
  - Fundamental
author:
  - "[[Aes Saputra]]"
url: https://aessaputra.net/notes/using-operators-in-your-programs
created: 2025-12-18
published: 2025-12-18
date: 2025-12-18
topics:
  - "[[Java]]"
  - "[[Programming Fundamentals]]"
status: "[[Published]]"
feed: show
---

## Operator

Sekarang setelah Anda mempelajari cara mendeklarasikan dan menginisialisasi variabel, Anda mungkin ingin tahu cara melakukan sesuatu dengan variabel tersebut. Mempelajari operator bahasa pemrograman Java adalah tempat yang baik untuk memulai. Operator adalah simbol khusus yang melakukan operasi tertentu pada satu, dua, atau tiga *operand*, dan kemudian mengembalikan hasilnya.

Saat kita menjelajahi operator bahasa pemrograman Java, mungkin berguna bagi Anda untuk mengetahui sebelumnya operator mana yang memiliki preseden (urutan prioritas) tertinggi. Operator dalam tabel berikut terdaftar berdasarkan urutan preseden. Semakin dekat ke bagian atas tabel operator muncul, semakin tinggi presedennya. Operator dengan preseden lebih tinggi dievaluasi sebelum operator dengan preseden yang relatif lebih rendah. Operator pada baris yang sama memiliki preseden yang sama. Ketika operator dengan preseden yang sama muncul dalam ekspresi yang sama, aturan harus mengatur mana yang dievaluasi terlebih dahulu. Semua operator biner kecuali operator penugasan dievaluasi dari kiri ke kanan; operator penugasan dievaluasi dari kanan ke kiri.

| Kategori Operator | Operator |
| :--- | :--- |
| postfix | `expr++` `expr--` |
| unary | `++expr` `--expr` `+expr` `-expr` `~` `!` |
| multiplicative | `*` `/` `%` |
| additive | `+` `-` |
| shift | `<<` `>>` `>>>` |
| relational | `<` `>` `<=` `>=` `instanceof` |
| equality | `==` `!=` |
| bitwise AND | `&` |
| bitwise exclusive OR | `^` |
| bitwise inclusive OR | `|` |
| logical AND | `&&` |
| logical OR | `||` |
| ternary | `? :` |
| assignment | `=` `+=` `-=` `*=` `/=` `%=` `&=` `^=` `|=` `<<=` `>>=` `>>>=` |

Dalam pemrograman tujuan umum, operator tertentu cenderung muncul lebih sering daripada yang lain; misalnya, operator penugasan `=` jauh lebih umum daripada operator *unsigned right shift* `>>>`. Dengan mengingat hal itu, pembahasan berikut berfokus pertama pada operator yang paling mungkin Anda gunakan secara teratur, dan diakhiri dengan berfokus pada mereka yang kurang umum. Setiap pembahasan disertai dengan kode sampel yang dapat Anda kompilasi dan jalankan. Mempelajari outputnya akan membantu memperkuat apa yang baru saja Anda pelajari.

## Operator Penugasan Sederhana

Salah satu operator paling umum yang akan Anda temui adalah operator penugasan sederhana `=`. Anda melihat operator ini di kelas `Bicycle`; operator ini menugaskan nilai di sebelah kanannya ke operand di sebelah kirinya:

```java
int cadence = 0;
int speed = 0;
int gear = 1;
```

Operator ini juga dapat digunakan pada objek untuk menugaskan referensi objek, seperti yang dibahas di bagian [[Creating Objects]].

## Operator Aritmatika

Bahasa pemrograman Java menyediakan operator yang melakukan penambahan, pengurangan, perkalian, dan pembagian. Ada kemungkinan besar Anda akan mengenalinya dari padanannya dalam matematika dasar. Satu-satunya simbol yang mungkin terlihat baru bagi Anda adalah `%`, yang membagi satu operand dengan yang lain dan mengembalikan sisanya sebagai hasilnya.

| Operator | Deskripsi |
| :--- | :--- |
| `+` | Operator aditif (juga digunakan untuk penggabungan String) |
| `-` | Operator pengurangan |
| `*` | Operator perkalian |
| `/` | Operator pembagian |
| `%` | Operator sisa bagi (remainder) |

Program berikut, `ArithmeticDemo`, menguji operator aritmatika:

```java
class ArithmeticDemo {

    public static void main (String[] args) {

        int result = 1 + 2;
        // result sekarang 3
        System.out.println("1 + 2 = " + result);
        int original_result = result;

        result = result - 1;
        // result sekarang 2
        System.out.println(original_result + " - 1 = " + result);
        original_result = result;

        result = result * 2;
        // result sekarang 4
        System.out.println(original_result + " * 2 = " + result);
        original_result = result;

        result = result / 2;
        // result sekarang 2
        System.out.println(original_result + " / 2 = " + result);
        original_result = result;

        result = result + 8;
        // result sekarang 10
        System.out.println(original_result + " + 8 = " + result);
        original_result = result;

        result = result % 7;
        // result sekarang 3
        System.out.println(original_result + " % 7 = " + result);
    }
}
```

Program ini mencetak output berikut:

```
1 + 2 = 3
3 - 1 = 2
2 * 2 = 4
4 / 2 = 2
2 + 8 = 10
10 % 7 = 3
```

Anda juga dapat menggabungkan operator aritmatika dengan operator penugasan sederhana untuk membuat **penugasan majemuk** (*compound assignments*). Misalnya, `x += 1;` dan `x = x + 1;` keduanya menambah nilai `x` sebesar 1.

Operator `+` juga dapat digunakan untuk menggabungkan (menyambung) dua string bersama-sama, seperti yang ditunjukkan dalam program `ConcatDemo` berikut:

```java
class ConcatDemo {
    public static void main(String[] args){
        String firstString = "This is";
        String secondString = " a concatenated string.";
        String thirdString = firstString+secondString;
        System.out.println(thirdString);
    }
}
```

Pada akhir program ini, variabel `thirdString` berisi "This is a concatenated string.", yang dicetak ke output standar.

## Operator Unary

Operator unary hanya membutuhkan satu operand; mereka melakukan berbagai operasi seperti menambah/mengurangi nilai sebesar satu, menegasikan ekspresi, atau membalikkan nilai boolean.

| Operator | Deskripsi |
| :--- | :--- |
| `+` | Operator unary plus; menunjukkan nilai positif (namun angka bernilai positif tanpa ini) |
| `-` | Operator unary minus; menegasikan ekspresi |
| `++` | Operator increment; menambah nilai sebesar 1 |
| `--` | Operator decrement; mengurangi nilai sebesar 1 |
| `!` | Operator logical complement; membalikkan nilai boolean |

Program `PrePostDemo` berikut mengilustrasikan operator prefix/postfix unary increment:

```java
class PrePostDemo {
    public static void main(String[] args){
        int i = 3;
        i++;
        // mencetak 4
        System.out.println(i);
        ++i;			   
        // mencetak 5
        System.out.println(i);
        // mencetak 6
        System.out.println(++i);
        // mencetak 6
        System.out.println(i++);
        // mencetak 7
        System.out.println(i);
    }
}
```

## Operator Kesetaraan dan Relasional

Operator kesetaraan dan relasional menentukan apakah satu operand lebih besar dari, lebih kecil dari, sama dengan, atau tidak sama dengan operand lainnya. Sebagian besar operator ini mungkin terlihat familier bagi Anda juga. Perlu diingat bahwa Anda harus menggunakan "==", bukan "=", ketika menguji apakah dua nilai primitif sama.

| Operator | Deskripsi |
| :--- | :--- |
| `==` | sama dengan |
| `!=` | tidak sama dengan |
| `>` | lebih besar dari |
| `>=` | lebih besar dari atau sama dengan |
| `<` | lebih kecil dari |
| `<=` | lebih kecil dari atau sama dengan |

Program `ComparisonDemo` berikut menguji operator perbandingan:

```java
class ComparisonDemo {

    public static void main(String[] args){
        int value1 = 1;
        int value2 = 2;
        if(value1 == value2)
            System.out.println("value1 == value2");
        if(value1 != value2)
            System.out.println("value1 != value2");
        if(value1 > value2)
            System.out.println("value1 > value2");
        if(value1 < value2)
            System.out.println("value1 < value2");
        if(value1 <= value2)
            System.out.println("value1 <= value2");
    }
}
```

Output:
```
value1 != value2
value1 < value2
value1 <= value2
```

## Operator Kondisional

Operator `&&` dan `||` melakukan operasi *Conditional-AND* dan *Conditional-OR* pada dua ekspresi boolean. Operator ini menunjukkan perilaku "short-circuiting", yang berarti operand kedua dievaluasi hanya jika diperlukan.

| Operator | Deskripsi |
| :--- | :--- |
| `&&` | Conditional-AND |
| `||` | Conditional-OR |
| `?:` | Ternary (singkatan untuk pernyataan if-then-else) |

Program `ConditionalDemo1` berikut menguji operator ini:

```java
class ConditionalDemo1 {

    public static void main(String[] args){
        int value1 = 1;
        int value2 = 2;
        if((value1 == 1) && (value2 == 2))
            System.out.println("value1 is 1 AND value2 is 2");
        if((value1 == 1) || (value2 == 1))
            System.out.println("value1 is 1 OR value2 is 1");
    }
}
```

Operator lain, `?:`, dapat dianggap sebagai singkatan untuk pernyataan `if-then-else`. Operator ini juga dikenal sebagai *ternary operator* karena menggunakan tiga operand.

```java
class ConditionalDemo2 {

    public static void main(String[] args){
        int value1 = 1;
        int value2 = 2;
        int result;
        boolean someCondition = true;
        result = someCondition ? value1 : value2;

        System.out.println(result);
    }
}
```

## Operator Perbandingan Tipe `instanceof`

Operator `instanceof` membandingkan objek dengan tipe tertentu. Anda dapat menggunakannya untuk menguji apakah suatu objek adalah instance dari kelas, instance dari subclass, atau instance dari kelas yang mengimplementasikan antarmuka tertentu.

```java
class InstanceofDemo {
    public static void main(String[] args) {

        Parent parent = new Parent();
        Parent child = new Child();

        System.out.println("parent instanceof Parent: "
            + (parent instanceof Parent));
        System.out.println("parent instanceof Child: "
            + (parent instanceof Child));
        System.out.println("parent instanceof MyInterface: "
            + (parent instanceof MyInterface));
        System.out.println("child instanceof Parent: "
            + (child instanceof Parent));
        System.out.println("child instanceof Child: "
            + (child instanceof Child));
        System.out.println("child instanceof MyInterface: "
            + (child instanceof MyInterface));
    }
}

class Parent {}
class Child extends Parent implements MyInterface {}
interface MyInterface {}
```

## Operator Bitwise dan Bit Shift

Bahasa pemrograman Java juga menyediakan operator yang melakukan operasi bitwise dan bit shift pada tipe integral. Operator yang dibahas di bagian ini lebih jarang digunakan. Oleh karena itu, pembahasannya singkat; tujuannya hanyalah untuk memberi tahu Anda bahwa operator ini ada.

| Operator | Deskripsi |
| :--- | :--- |
| `~` | Unary bitwise complement |
| `<<` | Signed left shift |
| `>>` | Signed right shift |
| `>>>` | Unsigned right shift |
| `&` | Bitwise AND |
| `^` | Bitwise exclusive OR |
| `|` | Bitwise inclusive OR |

Program `BitDemo` berikut menggunakan operator bitwise AND untuk mencetak angka "2" ke output standar.

```java
class BitDemo {
    public static void main(String[] args) {
        int bitmask = 0x000F;
        int val = 0x2222;
        // prints "2"
        System.out.println(val & bitmask);
    }
}
```

## Referensi

*   [Using Operators in Your Programs - Dev.java](https://dev.java/learn/language-basics/using-operators/)
*   [Summary of Operators - Dev.java](https://dev.java/learn/language-basics/all-operators/)
*   Topik terkait: [[Creating Arrays in Your Programs]], [[Using the Var Type Identifier]], [[Control Flow]], [[Tipe Data Primitif]].
