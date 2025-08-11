# S.O. 2025.1 - Atividade 2.02 - Gestão de memória

## Informações gerais

- **Objetivo do repositório**: Repositório para atividade avaliativa dos alunos
- **Assunto**: Gestão de memória
- **Público alvo**: alunos da disciplina de SO (Sistemas Operacionais) do curso de TADS (Superior em Tecnologia em Análise e Desenvolvimento de Sistemas) no CNAT-IFRN (Instituto Federal de Educação, Ciência e Tecnologia do Rio Grande do Norte - Campus Natal-Central).
- disciplina: **SO** [Sistemas Operacionais](https://github.com/sistemas-operacionais/)
- professor: [Leonardo A. Minora](https://github.com/leonardo-minora)
- aluno: [Gabriel Henrique Furtado Barbosa] (https://github.com/gbrielf)
- Repositótio do aluno: FIXME

## Tarefas do aluno
1. Fork desse repositório e atualizar a linha 10 com o nome e link do github
2. Ler a descrição da atividade
3. Montar a resposta no final deste arqivo, no tópico **Resposta**

---

## 1. Descrição da atividade
### 1.1. Objetivo
Praticar os conceitos de alocação de memória (best-fit), memória virtual e desfragmentação em um sistema com memória limitada.

---

### 1.2. Contexto
Um computador possui apenas **64 KB de RAM** e um **disco rígido para memória virtual**. O sistema operacional deve gerenciar 5 processos com tamanhos diferentes, cuja soma ultrapassa a capacidade da RAM.

#### 1.2.1. Processos iniciais

| Processo | Tamanho (KB) |
|----------|-------------|
| P1       | 20          |
| P2       | 15          |
| P3       | 25          |
| P4       | 10          |
| P5       | 18          |
| **Total**| **88 KB**   |

- **Memória RAM**: 64 KB (contígua, inicialmente vazia).  
- **Memória Virtual (Disco)**: Espaço ilimitado para paginação.

#### 1.2.2. Alocação Inicial com Best-Fit
Os alunos devem simular a alocação dos processos na RAM usando o algoritmo **best-fit**.  
- A memória RAM será representada como um bloco contíguo (ex: `[0KB - 64KB]`).  
- Devem alocar os processos nos menores espaços livres que atendam ao seu tamanho.  

**Alocação inicial**:  
1. P1 (20 KB) → Ocupa [0-20].  
2. P2 (15 KB) → Ocupa [20-15].  
3. _continuar a partir daqui_

#### 1.2.3. Simular Memória Virtual (Paginação)
- Os processos não alocados na RAM devem ser "paginados" no disco.  
- Criar uma tabela de páginas indicando quais partes estão na RAM e quais estão no disco.  

#### 1.2.4. Desfragmentação da RAM
- Desfragmentar a RAM para liberar espaço contíguo.
- Após desfragmentação (compactação), verificar quais processos podem ser alocado.  

### 1.3. Questões para Reflexão
1. Best-fit foi mais eficiente que first-fit ou worst-fit neste cenário?  
2. Como a memória virtual evitou um deadlock?  
3. Qual o impacto da desfragmentação no desempenho do sistema?  

---

## Resposta

### 1. Alocação Inicial com Best-Fit

| Processo | Tamanho (KB) |
|----------|--------------|
| P1       | 20           |
| P2       | 15           |
| P3       | 25           |
| P4       | 10           |
| P5       | 18           |

**Passo a passo da alocação (Best-Fit):**
1. **P1 (20KB)** → ocupa `[0 – 20]` (44 KB livres)
2. **P2 (15KB)** → ocupa `[20 – 35]` (29 KB livres)
3. **P3 (25KB)** → ocupa `[35 – 60]` (4 KB livres)
4. **P4 (10KB)** → não cabe, vai para disco
5. **P5 (18KB)** → não cabe, vai para disco

### 2. Simular Memória Virtual (Paginação)

| Processo | Tamanho (KB) | RAM (KB) | Disco |
|----------|--------------|----------|-------|
| P1       | 20           | 0–20     | -     |
| P2       | 15           | 20–35    | -     |
| P3       | 25           | 35–60    | -     |
| P4       | 10           | -        | Total |
| P5       | 18           | -        | Total |

### 3. Desfragmentação da 

**Antes da desfragmentação:** [0–20: P1] [20–35: P2] [35–60: P3] [60–64: Livre]
**Depois da desfragmentação:** [0–60: P1, P2, P3] [60–64: Livre]

 ### 4. Questões para Reflexão


**Best-fit foi mais eficiente que first-fit ou worst-fit neste cenário?**  
Sim. O Best-Fit reduziu o desperdício interno, alocando os processos nos menores blocos possíveis, mas a limitação física da RAM impediu que todos os processos fossem alocados.

**Como a memória virtual evitou um deadlock?**  
A paginação para o disco permitiu a execução de processos que não cabiam na RAM, evitando bloqueios por falta de espaço.

**Qual o impacto da desfragmentação no desempenho do sistema?**  
A desfragmentação melhora a utilização da memória ao remover a fragmentação externa, mas exige movimentação de dados na RAM, o que consome tempo e recursos do processador.