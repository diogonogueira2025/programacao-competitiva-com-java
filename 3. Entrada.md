# Entrada

### Entrada básica
A entrada do programa geralmente consiste em números e strings separados por espaços e quebras de linha. Eles podem ser lidos da seguinte forma:

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
  
public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader in = new BufferedReader(
            new InputStreamReader(System.in)
        );
        
        // entrada: "123 456 monkey"
        String[] tokens = in.readLine().trim().split(" ");

        int a = Integer.parseInt(tokens[0]);  // 123
        int b = Integer.parseInt(tokens[1]);  // 456
        String x = tokens[2];                 // "monkey"

        in.close();
    }
}
```

---

Explicação:

**Imports**

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;
```

As três classes precisam ser importadas explicitamente:
- `BufferedReader` — lê texto de forma eficiente, linha por linha
- `InputStreamReader` — faz a ponte entre o fluxo de bytes brutos (`System.in`) e caracteres legíveis
- `IOException` — exceção que pode ser lançada durante operações de I/O

---

**Criação do leitor**

```java
BufferedReader in = new BufferedReader(
    new InputStreamReader(System.in)
);
```

`System.in` é a entrada padrão (o teclado, ou o arquivo de entrada do juiz). O `InputStreamReader` converte esses bytes em caracteres, e o `BufferedReader` os agrupa em linhas. Os dois são encadeados — é o padrão idiomático de I/O em Java.

---

**Leitura e divisão da linha**

```java
String[] tokens = in.readLine().trim().split(" ");
```

- `readLine()` lê a linha inteira como uma String — por exemplo, `"123 456 monkey"`. 
- `trim()` remove espaços e o `\r` das bordas, que pode aparecer em juízes. 
- `split(" ")` divide a linha em cada espaço, produzindo o vetor `["123", "456", "monkey"]`.

---

**Conversão e atribuição**

```java
int a = Integer.parseInt(tokens[0]);  // 123
int b = Integer.parseInt(tokens[1]);  // 456
String x = tokens[2];                 // "monkey"
```

Tudo que vem da entrada é String. Números precisam ser convertidos explicitamente com `Integer.parseInt()`. Strings podem ser atribuídas diretamente.

---

**Fechamento do leitor**

```java
in.close();
```

Libera o recurso de I/O. Em competições raramente causa problema omitir, mas é boa prática manter.