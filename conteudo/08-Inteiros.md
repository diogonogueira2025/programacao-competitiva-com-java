# Inteiros
O tipo inteiro mais usado em programação competitiva com Java é o `int`, que é um tipo de 32 bits com um intervalo de valores de −2³¹ ... 2³¹−1, ou aproximadamente −2·10⁹ ... 2·10⁹. Se o tipo `int` não for suficiente, o tipo de 64 bits `long` pode ser usado. Ele tem um intervalo de valores de −2⁶³ ... 2⁶³−1, ou aproximadamente −9·10¹⁸ ... 9·10¹⁸.

O código a seguir define uma variável `int`:

```java
int x = 2147483647;
```

O código a seguir define uma variável `long`:

```java
long x = 123456789123456789L;
```

O sufixo `L` indica que o literal é do tipo `long`.

Um erro comum ao usar o tipo `long` é que o tipo `int` ainda é usado em algum lugar do código. Por exemplo, o código a seguir contém um erro sutil:

```java
int a = 123456789;
long b = a * a;
System.out.println(b); // -1757895751
```

Mesmo que a variável `b` seja do tipo `long`, os dois números na expressão `a*a` são do tipo `int`, e o resultado também é do tipo `int`. Por causa disso, a variável `b` vai conter um resultado errado. O problema pode ser resolvido trocando o tipo de `a` para `long` ou fazendo um cast na expressão:

```java
long b = (long) a * a;
```