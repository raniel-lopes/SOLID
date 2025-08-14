# Apostila de Estudos: Princípios SOLID  
**Disciplina:** Programação Orientada a Objetos Avançada  
**Curso:** Engenharia de Software  

---

## Sumário

1. Introdução ao SOLID
2. Princípio da Responsabilidade Única (SRP)
3. Princípio do Aberto/Fechado (OCP)
4. Princípio da Substituição de Liskov (LSP)
5. Princípio da Segregação de Interfaces (ISP)
6. Princípio da Inversão de Dependência (DIP)
7. Exercícios práticos
8. Referências

---

## 1. Introdução ao SOLID

SOLID é um acrônimo para cinco princípios de design de código orientado a objetos, propostos por Robert C. Martin ("Uncle Bob"), que visam tornar o software mais compreensível, flexível e de fácil manutenção.

- **Single Responsibility Principle (SRP)**
- **Open/Closed Principle (OCP)**
- **Liskov Substitution Principle (LSP)**
- **Interface Segregation Principle (ISP)**
- **Dependency Inversion Principle (DIP)**

---

## 2. Princípio da Responsabilidade Única (SRP)

**Definição:**  
Uma classe deve ter apenas um motivo para mudar, ou seja, ela deve ter apenas uma responsabilidade.

**Exemplo:**
```java
// Violando SRP
class Relatorio {
    void gerarRelatorio() { /* ... */ }
    void salvarNoBanco() { /* ... */ }
    void enviarPorEmail() { /* ... */ }
}

// Aplicando SRP
class GeradorRelatorio {
    void gerar() { /* ... */ }
}

class RelatorioRepositorio {
    void salvar() { /* ... */ }
}

class EmailService {
    void enviar() { /* ... */ }
}
```

**Vantagens:**  
- Facilita manutenção e testes  
- Reduz acoplamento

**Desvantagens:**  
- Pode aumentar o número de classes

---

## 3. Princípio do Aberto/Fechado (OCP)

**Definição:**  
Entidades de software (classes, módulos, funções, etc.) devem estar abertas para extensão, mas fechadas para modificação.

**Exemplo:**
```java
// Violando OCP
class Calculadora {
    int calcular(String operacao, int a, int b) {
        if (operacao.equals("soma")) return a + b;
        if (operacao.equals("subtrai")) return a - b;
        // etc.
    }
}

// Aplicando OCP
interface Operacao {
    int executar(int a, int b);
}

class Soma implements Operacao {
    int executar(int a, int b) { return a + b; }
}

class Subtrai implements Operacao {
    int executar(int a, int b) { return a - b; }
}

class Calculadora {
    int calcular(Operacao op, int a, int b) {
        return op.executar(a, b);
    }
}
```

**Vantagens:**  
- Facilita adição de novas funcionalidades  
- Reduz risco de bugs ao modificar código já testado

---

## 4. Princípio da Substituição de Liskov (LSP)

**Definição:**  
Subtipos devem ser substituíveis por seus tipos base sem alterar o comportamento esperado do programa.

**Exemplo:**
```java
class Ave {
    void voar() { /* ... */ }
}

class Pinguim extends Ave {
    void voar() { throw new UnsupportedOperationException(); }
}
```
Neste caso, `Pinguim` não deveria herdar de `Ave` se não pode voar.

**Vantagens:**  
- Garante polimorfismo seguro  
- Evita bugs inesperados

---

## 5. Princípio da Segregação de Interfaces (ISP)

**Definição:**  
Uma classe não deve ser forçada a implementar interfaces que não utiliza.

**Exemplo:**
```java
// Violando ISP
interface Trabalhador {
    void trabalhar();
    void comer();
}

class Robo implements Trabalhador {
    void trabalhar() { /* ... */ }
    void comer() { /* Não faz sentido para robô */ }
}

// Aplicando ISP
interface Trabalhador {
    void trabalhar();
}

interface Eater {
    void comer();
}

class Robo implements Trabalhador {
    void trabalhar() { /* ... */ }
}
```

---

## 6. Princípio da Inversão de Dependência (DIP)

**Definição:**  
Dependa de abstrações e não de implementações concretas.

**Exemplo:**
```java
// Violando DIP
class Lampada {
    void acender() { /* ... */ }
}

class Interruptor {
    private Lampada lampada;
    void ligar() { lampada.acender(); }
}

// Aplicando DIP
interface Dispositivo {
    void ligar();
}

class Lampada implements Dispositivo {
    void ligar() { /* ... */ }
}

class Interruptor {
    private Dispositivo dispositivo;
    void ligar() { dispositivo.ligar(); }
}
```

---

## 7. Exercícios práticos

1. Identifique violações dos princípios SOLID em um código legado e proponha melhorias.
2. Implemente um sistema de cadastro de usuários aplicando todos os princípios SOLID.
3. Refaça exemplos do seu projeto de POO usando SOLID.

---

## 8. Referências

- Clean Code e Clean Architecture, Robert C. Martin
- [Artigo original de Uncle Bob sobre SOLID](https://blog.cleancoder.com/uncle-bob/2014/05/08/SingleReponsibilityPrinciple.html)
- [SOLID Principles — Devopedia](https://devopedia.org/solid-principles)
- [SOLID Principles — DigitalOcean](https://www.digitalocean.com/community/tutorials/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)

---
