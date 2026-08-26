# Exemplo de derivação sintática: `for` em Java

**Objetivo:** mostrar como um pequeno trecho de código pode ser construído a partir de regras gramaticais de uma linguagem real.

**Fonte de referência:** Java Language Specification (JLS), seção **14.14.1 – The basic for Statement**. A gramática apresentada abaixo foi simplificada para fins didáticos, preservando a estrutura sintática essencial do comando `for`.

## 1. Código gerado

```java
public class ExemploFor {
    public static void main(String[] args) {
        for (int i = 1; i <= 5; i++) {
            System.out.println(i);
        }
    }
}
```

A derivação será concentrada especificamente no seguinte trecho:

```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```

## 2. Regras gramaticais utilizadas

Para concentrar a derivação no comando de repetição, utilizamos uma gramática reduzida. Os símbolos entre `< >` representam **não terminais**, enquanto os demais elementos representam **terminais** da linguagem.

```text
<for_statement> ::= for ( <for_init> ; <expression> ; <for_update> ) <statement>

<for_init> ::= <local_variable_declaration>

<local_variable_declaration> ::= int <identifier> = <expression>

<expression> ::= <integer_literal>
               | <identifier>
               | <identifier> <= <integer_literal>

<for_update> ::= <identifier> ++

<statement> ::= <block>

<block> ::= { <statement_list> }

<statement_list> ::= <statement_expression> ;

<statement_expression> ::= System.out.println ( <expression> )

<identifier> ::= i

<integer_literal> ::= 1 | 5
```

A regra `<for_statement>` representa a estrutura principal do `for` em Java. Ela determina a existência de uma inicialização, uma condição, uma atualização e um comando que será executado durante a repetição.

A regra `<local_variable_declaration>` permite declarar e inicializar a variável `i`. A `<expression>` permite representar os valores e a condição `i <= 5`. Já `<for_update>` representa o incremento `i++`.

## 3. Derivação

A derivação começa no símbolo não terminal `<for_statement>` e substitui, passo a passo, cada não terminal até obter a sequência de terminais correspondente ao trecho desejado.

```text
<for_statement>

⇒ for ( <for_init> ; <expression> ; <for_update> ) <statement>

⇒ for ( <local_variable_declaration> ; <expression> ; <for_update> ) <statement>

⇒ for ( int <identifier> = <expression> ; <expression> ; <for_update> ) <statement>

⇒ for ( int i = <expression> ; <expression> ; <for_update> ) <statement>

⇒ for ( int i = <integer_literal> ; <expression> ; <for_update> ) <statement>

⇒ for ( int i = 1 ; <expression> ; <for_update> ) <statement>

⇒ for ( int i = 1 ; <identifier> <= <integer_literal> ; <for_update> ) <statement>

⇒ for ( int i = 1 ; i <= <integer_literal> ; <for_update> ) <statement>

⇒ for ( int i = 1 ; i <= 5 ; <for_update> ) <statement>

⇒ for ( int i = 1 ; i <= 5 ; <identifier> ++ ) <statement>

⇒ for ( int i = 1 ; i <= 5 ; i ++ ) <statement>

⇒ for ( int i = 1 ; i <= 5 ; i ++ ) <block>

⇒ for ( int i = 1 ; i <= 5 ; i ++ ) { <statement_list> }

⇒ for ( int i = 1 ; i <= 5 ; i ++ ) { <statement_expression> ; }

⇒ for ( int i = 1 ; i <= 5 ; i ++ ) { System.out.println ( <expression> ) ; }

⇒ for ( int i = 1 ; i <= 5 ; i ++ ) { System.out.println ( <identifier> ) ; }

⇒ for ( int i = 1 ; i <= 5 ; i ++ ) { System.out.println ( i ) ; }
```

### Forma concreta em Java

```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```

## 4. Símbolos terminais e não terminais

Os **não terminais** são símbolos que podem ser substituídos por outras regras durante a derivação. Entre os utilizados neste exemplo estão:

- `<for_statement>`
- `<for_init>`
- `<local_variable_declaration>`
- `<expression>`
- `<for_update>`
- `<statement>`
- `<block>`
- `<statement_list>`
- `<statement_expression>`
- `<identifier>`
- `<integer_literal>`

Os **terminais** são elementos que aparecem efetivamente no código Java:

- `for`
- `(`
- `)`
- `int`
- `i`
- `=`
- `1`
- `;`
- `<=`
- `5`
- `++`
- `{`
- `}`
- `System.out.println`

## 5. Breve explicação textual

O comando `for` em Java é uma estrutura de repetição que permite executar um bloco de código enquanto determinada condição for verdadeira.

Neste exemplo, `int i = 1` declara a variável de controle `i` e define seu valor inicial como 1. A expressão `i <= 5` determina que a repetição deve continuar enquanto `i` for menor ou igual a 5. A expressão `i++` incrementa o valor da variável após cada repetição.

Dentro do bloco delimitado por `{` e `}`, o comando `System.out.println(i);` apresenta o valor atual da variável `i`.

A derivação demonstra que esse trecho não é uma sequência arbitrária de palavras e símbolos. Ele é sintaticamente válido porque pode ser obtido por substituições sucessivas a partir das regras da gramática da linguagem Java.

## Referência

**Oracle. Java Language Specification.**  
Seção 14.14.1 – *The basic for Statement*.  
Disponível em: https://docs.oracle.com/javase/specs/jls/se25/html/jls-14.html#jls-14.14.1
