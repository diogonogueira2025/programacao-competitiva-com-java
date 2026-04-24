# BigInteger
Normalmente, os problemas de competição são formulados de forma que o tipo `long` seja suficiente. Porém, ao contrário do g++ em C++, **Java não possui um tipo inteiro nativo de 128 bits**. Se você precisar de precisão além do `long`, a alternativa é usar `BigInteger`, da biblioteca `java.math`:

```java
import java.math.BigInteger;

BigInteger a = new BigInteger("123456789123456789123456789");
BigInteger b = a.multiply(a);
System.out.println(b);
```


**Criando um BigInteger**

```java
import java.math.BigInteger;

BigInteger a = new BigInteger("123456789123456789123456789");
BigInteger b = BigInteger.valueOf(42L); // a partir de um long
```

Não é possível usar literais diretamente (`123456789...`), sempre precisa passar como `String` ou converter de um `long`.

---

**Constantes úteis**

```java
BigInteger.ZERO  // 0
BigInteger.ONE   // 1
BigInteger.TWO   // 2
BigInteger.TEN   // 10
```

Prefira essas constantes a criar `new BigInteger("0")` à toa.

---

**Operações aritméticas**

Como `BigInteger` é imutável, toda operação retorna um **novo objeto**:

```java
BigInteger a = new BigInteger("100");
BigInteger b = new BigInteger("30");

a.add(b);        // 130
a.subtract(b);   // 70
a.multiply(b);   // 3000
a.divide(b);     // 3  (divisão inteira)
a.remainder(b);  // 10 (resto)
a.mod(b);        // 10 (semelhante ao remainder, mas sempre positivo)
a.pow(3);        // 1000000 (a³)
a.negate();      // -100
a.abs();         // valor absoluto
```

---

**Comparação**

Nunca use `==` para comparar `BigInteger` — compare com `.equals()` ou `.compareTo()`:

```java
a.equals(b);       // true/false
a.compareTo(b);    // -1 se a < b, 0 se a == b, 1 se a > b

BigInteger.ZERO.equals(a); // verificar se é zero
a.signum();                // -1, 0 ou 1 (sinal do número)
```

---

**Operações úteis em competitivo**

```java
a.gcd(b);              // MDC entre a e b
a.isProbablePrime(10); // teste de primalidade probabilístico
a.nextProbablePrime(); // próximo provável primo a partir de a
a.max(b);              // maior entre a e b
a.min(b);              // menor entre a e b
a.bitCount();          // número de bits 1 na representação
a.bitLength();         // número de bits necessários para representar
```

---

**Conversões**

```java
// BigInteger -> primitivos
int    i = a.intValue();    // cuidado: trunca se não couber
long   l = a.longValue();   // cuidado: trunca se não couber
double d = a.doubleValue();

// BigInteger -> String
String s = a.toString();     // base 10
String s = a.toString(2);    // base 2 (binário)
String s = a.toString(16);   // base 16 (hexadecimal)

// String -> BigInteger
BigInteger x = new BigInteger("ff", 16); // lendo em hex
BigInteger y = new BigInteger("1010", 2); // lendo em binário
```

---

**Cuidado com performance**

`BigInteger` é **muito mais lento** que `int` e `long`. Em problemas com muitas operações em loop, pode causar TLE facilmente. Use apenas quando o enunciado deixar claro que os valores ultrapassam o limite do `long` — caso contrário, prefira sempre `long`.