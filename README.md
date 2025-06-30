
# 🧪 Sistema de Gerenciamento de Exames Médicos – IF Diagnósticos

Este projeto é parte da disciplina de **Padrões de Projeto**, com o objetivo de desenvolver um sistema flexível, extensível e de fácil manutenção para o gerenciamento de exames médicos e emissão de laudos.

---

## 📌 Objetivo

Atender os requisitos da empresa **IF Diagnósticos**, simulando um sistema real que permita:

- Gerenciar diferentes tipos de exames (Hemograma, Ultrassonografia, Ressonância...)
- Validar os exames com regras específicas
- Gerar laudos em múltiplos formatos (Texto, HTML, PDF)
- Notificar o paciente automaticamente
- Calcular preços com descontos dinâmicos
- Processar exames com diferentes níveis de urgência

---

## 📘 Requisitos Funcionais Atendidos

- **R1**: Leitura de dados via CSV  
- **R2**: Geração de número sequencial único de exames  
- **R3**: Inclusão de novos tipos de exame sem impactar o código  
- **R4**: Geração de laudos em múltiplos formatos  
- **R5**: Regras de validação específicas por tipo de exame  
- **R6**: Notificações via WhatsApp (e futuros canais)  
- **R7**: Políticas de desconto configuráveis  
- **R8**: Processamento por prioridade (URGENTE > POUCO_URGENTE > ROTINA)  
- **R9**: Programa principal com simulação de execução  
- **R10**: (Extra) Possibilidade de uso de Decorator ou Proxy para extensões futuras  

---

## 🧩 Padrões de Projeto Utilizados

### ✅ Singleton
- **Classe:** `Sequencer`
- **Função:** Garante a geração única de IDs para exames (R2)

```java
int nextId = Sequencer.getInstance().next();
```

### ✅ Factory Method / Abstract Factory
- **Classes:** `ExamFactory`, `FormatterFactory`, `NotifierFactory`, `ValidationFactory`, `DiscountFactory`
- **Função:** Facilita a criação extensível de objetos com múltiplas variações (R3–R7)

```java
Exam exam = ExamFactory.create("hemogram", ...);
ReportFormatter formatter = FormatterFactory.get("pdf");
```

### ✅ Strategy
- **Interfaces:** `ValidationStrategy`, `ReportFormatter`, `Notifier`, `DiscountPolicy`
- **Função:** Permite trocar comportamentos como validação, formatação, notificações e descontos em tempo de execução (R4–R7)

```java
DiscountPolicy policy = DiscountFactory.get("convenio");
BigDecimal finalValue = policy.apply(baseValue);
```

### ✅ Priority Queue
- **Classe:** `ExamQueue`
- **Função:** Controla a ordem de processamento dos exames baseado em sua urgência (R8)

```java
queue.enqueue(exameUrgente);
Exam next = queue.dequeue(); // sempre retorna o exame mais prioritário
```

### ✅ Facade
- **Classe:** `ExamService`
- **Função:** Centraliza toda a lógica do sistema em uma interface simples para o programa principal (R9)

```java
ExamService service = new ExamService();
service.registerExam(...);
service.processNextExam();
```

### ✅ Proxy ou Decorator (sugestão para R10)
- **Função:** Pode ser usado futuramente para cache de laudos (Proxy) ou para empilhar descontos (Decorator)

```java
DiscountPolicy combinado = new OutubroRosaDiscount(new ConvenioDiscount());
```

---

## 🗂️ Organização do Projeto

```
src/
├── exam/                  # Tipos de exames
├── validation/            # Estratégias de validação
├── report/                # Geradores de laudos (HTML, texto, PDF)
├── notify/                # Estratégias de notificação (WhatsApp, etc.)
├── discount/              # Estratégias de desconto
├── factory/               # Fábricas de criação de objetos
├── service/               # Classe fachada com fluxo principal
└── util/                  # Singleton Sequencer e helpers
```

---

## 🖼️ Diagrama de Classes

![Diagrama de Classes](Class_Diagram_ST_Diagnosticos.svg)

---

## 📥 Repositório

🔗 Repositório GitHub:  
**https://github.com/gabrielmana6/ST-Diagnosticos**

---

## 👨‍🏫 Projeto acadêmico – Disciplina: Padrões de Projeto  
**Professor:** Alex Sandro C. Rêgo  
**Curso:** Sistemas para Internet  
