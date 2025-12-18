---
title: Pernyataan Kontrol Alur
aliases:
  - Java Control Flow
  - Control Flow Statements
categories:
  - "[[Posts]]"
tags:
  - Java
  - Programming
  - Fundamental
author:
  - "[[Aes Saputra]]"
url: https://aessaputra.github.io/notes/pernyataan-kontrol-alur/
created: 2025-12-18
published: 2025-12-18
date: 2025-12-18
topics:
  - "[[Java]]"
  - "[[Programming Fundamentals]]"
status: "[[Published]]"
feed: show
---

Pernyataan dalam kode sumber Java umumnya dieksekusi dari atas ke bawah, sesuai urutan kemunculannya. Namun, **Pernyataan Kontrol Alur** (Control Flow Statements) memecah aliran eksekusi linier ini dengan menggunakan pengambilan keputusan, perulangan, dan percabangan, memungkinkan program Anda untuk mengeksekusi blok kode tertentu secara kondisional. Artikel ini membahas pernyataan kontrol alur berdasarkan panduan resmi dari [[Dev.java]].

## Pernyataan If-Then dan If-Then-Else

### Pernyataan If-Then
Pernyataan `if-then` adalah pernyataan kontrol alur yang paling mendasar. Pernyataan ini memerintahkan program untuk mengeksekusi bagian kode tertentu hanya jika pengujian tertentu bernilai `true`.

Contoh implementasi pada kelas `Bicycle`:

```java
void applyBrakes() {
    // klausa "if": sepeda harus bergerak
    if (isMoving){ 
        // klausa "then": kurangi kecepatan saat ini
        currentSpeed--;
    }
}
```

Jika pengujian ini bernilai `false` (artinya sepeda tidak bergerak), kontrol akan melompat ke akhir pernyataan `if-then`.

### Pernyataan If-Then-Else
Pernyataan `if-then-else` menyediakan jalur eksekusi sekunder ketika klausa `if` bernilai `false`.

```java
void applyBrakes() {
    if (isMoving) {
        currentSpeed--;
    } else {
        System.err.println("The bicycle has already stopped!");
    }
}
```

### If-Then-Else Bertingkat
Anda dapat menggunakan rangkaian pernyataan `if-then-else` untuk menangani berbagai kondisi.

```java
class IfElseDemo {
    public static void main(String[] args) {
        int testscore = 76;
        char grade;

        if (testscore >= 90) {
            grade = 'A';
        } else if (testscore >= 80) {
            grade = 'B';
        } else if (testscore >= 70) {
            grade = 'C';
        } else if (testscore >= 60) {
            grade = 'D';
        } else {
            grade = 'F';
        }
        System.out.println("Grade = " + grade);
    }
}
```

## Pernyataan Switch

Pernyataan `switch` memungkinkan percabangan alur program berdasarkan nilai variabel. Untuk pembahasan lebih mendalam mengenai topik ini, silakan lihat artikel [[Pernyataan Switch]].

## Pernyataan While dan Do-While

### Pernyataan While
Pernyataan `while` terus mengeksekusi blok pernyataan selama kondisi tertentu bernilai `true`.

```java
class WhileDemo {
    public static void main(String[] args){
        int count = 1;
        while (count < 11) {
            System.out.println("Count is: " + count);
            count++;
        }
    }
}
```

### Pernyataan Do-While
Perbedaan utama antara `do-while` dan `while` adalah `do-while` mengevaluasi ekspresinya di bagian bawah loop. Oleh karena itu, pernyataan di dalam blok `do` selalu dieksekusi setidaknya satu kali.

```java
class DoWhileDemo {
    public static void main(String[] args){
        int count = 1;
        do {
            System.out.println("Count is: " + count);
            count++;
        } while (count < 11);
    }
}
```

## Pernyataan For

Pernyataan `for` menyediakan cara yang ringkas untuk melakukan iterasi pada rentang nilai. Programmer sering menyebutnya sebagai "for loop".

### Bentuk Dasar
```java
class ForDemo {
    public static void main(String[] args){
         for(int i=1; i<11; i++){
              System.out.println("Count is: " + i);
         }
    }
}
```

### Pernyataan For yang Ditingkatkan (Enhanced For Loop)
Didesain untuk iterasi melalui [[Collections Framework|koleksi]] dan [[Array|array]], bentuk ini lebih ringkas dan mudah dibaca.

```java
class EnhancedForDemo {
    public static void main(String[] args){
         int[] numbers = {1,2,3,4,5,6,7,8,9,10};
         for (int item : numbers) {
             System.out.println("Count is: " + item);
         }
    }
}
```

## Pernyataan Percabangan

Pernyataan percabangan memungkinkan Anda untuk mengalihkan aliran kontrol secara spesifik.

*   **`break`**: Mengakhiri loop `for`, `while`, atau `do-while` terdekat.
*   **`continue`**: Melewatkan iterasi saat ini dari loop dan melanjutkan ke iterasi berikutnya.
*   **`return`**: Keluar dari metode saat ini dan mengembalikan kontrol ke pemanggil metode.

## Referensi

*   [Control Flow Statements - Dev.java](https://dev.java/learn/language-basics/controlling-flow/)
*   [The Java™ Language Specification](https://docs.oracle.com/javase/specs/)
