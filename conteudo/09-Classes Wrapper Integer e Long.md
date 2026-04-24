# Classe Wrapper Integer e Long

Em Java, cada tipo primitivo possui uma **classe wrapper** correspondente no pacote `java.lang`. Para `int` e `long`, essas classes são `Integer` e `Long`, respectivamente. Além de permitirem o uso de tipos genéricos (como `List<Integer>`), elas expõem uma série de constantes e métodos estáticos muito úteis no dia a dia e na programação competitiva.

---

**Constantes de limite**

```java
System.out.println(Integer.MAX_VALUE); //  2147483647  ( 2³¹ - 1)
System.out.println(Integer.MIN_VALUE); // -2147483648  (-2³¹    )
System.out.println(Long.MAX_VALUE);    //  9223372036854775807  ( 2⁶³ - 1)
System.out.println(Long.MIN_VALUE);    // -9223372036854775808  (-2⁶³    )
```

Essas constantes são muito práticas em competitivo, por exemplo ao inicializar uma variável de mínimo/máximo:

```java
long min = Long.MIN_VALUE;
long max = Long.MAX_VALUE;
```

---

**Conversão de String para número**

```java
int a  = Integer.parseInt("42");
long b = Long.parseLong("123456789123456789");
```

---

**Conversão de número para String**

```java
String s = Integer.toString(42);    // "42"
String s = Long.toString(123456L);  // "123456"
```

Ou simplesmente usar `String.valueOf(n)`, que funciona pra qualquer tipo.

---

**Outras operações úteis**

```java
// Valor máximo/mínimo entre dois números
int maior = Integer.max(a, b);
int menor = Integer.min(a, b);

// Representação em outras bases
String binario = Integer.toBinaryString(10); // "1010"
String hex     = Integer.toHexString(255);   // "ff"
String octal   = Integer.toOctalString(8);   // "10"

// Contar bits ligados (útil em bitmask DP)
int bits = Integer.bitCount(7); // 3, pois 7 = 0b111
```

---

**Autoboxing e Unboxing**

O Java converte automaticamente entre o primitivo e o wrapper quando necessário:

```java
List<Integer> lista = new ArrayList<>();
lista.add(42);       // autoboxing:   int -> Integer
int x = lista.get(0); // unboxing: Integer -> int
```

Mas cuidado: em loops muito pesados, arrays primitivos (`int[]`, `long[]`) **tendem** a ser melhor do que `List<Integer>`.