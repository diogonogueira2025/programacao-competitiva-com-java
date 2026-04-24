# Problema: Verificando Overflow na Multiplicação

Dado um número inteiro $x$, determine se é possível multiplicá-lo por $10$ sem que ocorra overflow para o tipo `long`. Para cada valor de entrada, imprima o resultado da multiplicação ou `Nao eh possivel` caso o resultado ultrapasse o limite do tipo.

**Entrada**

Cada linha contém um inteiro $x$, onde $-2^{63} \leq x \leq 2^{63}-1$. Leia até EOF.

**Saída**

Para cada valor de entrada, imprima $x \times 10$ ou `Nao eh possivel`, um por linha.

**Exemplo de entrada**

```
5
-9223372036854775808
9223372036854775807
-1
```

**Exemplo de saída**

```
50
Nao eh possivel
Nao eh possivel
-10
```

### Resolução

Para verificar se $x \times 10$ causa overflow, precisamos garantir que o resultado esteja dentro dos limites do tipo `long`. Isso nos dá duas condições:

$$x \times 10 \leq 2^{63} - 1$$

$$x \times 10 \geq -2^{63}$$

Porém, **não podemos fazer essa multiplicação diretamente** — é exatamente ela que queremos evitar, pois se $x$ for grande o suficiente, `x * 10` já estoura antes mesmo da comparação acontecer.

A solução é isolar o x em cada condição, dividindo ambos os lados por 10. Fazemos isso separadamente para o limite superior e o limite inferior:

$$x \times 10 \leq 2^{63} - 1 \implies x \leq \dfrac{2^{63} - 1}{10}$$

$$x \times 10 \geq -2^{63} \implies x \geq \dfrac{-2^{63}}{10}$$

Dessa forma, teremos o intervalo:

$$\dfrac{-2^{63}}{10} \leq x \leq \dfrac{2^{63} - 1}{10}$$

Agora a verificação é feita **apenas com divisão**, que é segura, e aí sim podemos realizar a multiplicação com segurança:

```java
public static boolean verificarMult(long x) { 
	return x <= Long.MAX_VALUE / 10L && x >= Long.MIN_VALUE / 10L; 
}
```

**Código**

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader in = new BufferedReader(
            new InputStreamReader(System.in)
        );

        StringBuilder sb = new StringBuilder();
        String linha;

        while ((linha = in.readLine()) != null) {
            long x = Long.parseLong(linha);

            if (verificarMult(x)) {
                sb.append(x * 10L).append("\n");
            } else {
                sb.append("Nao eh possivel\n");
            }
        }

        System.out.print(sb);
        in.close();
    }

    public static boolean verificarMult(long x) {
        return x <= Long.MAX_VALUE / 10L && x >= Long.MIN_VALUE / 10L;
    }
}
```
