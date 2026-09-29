# Desafio-de-Projeto---Gerador-de-Curr-culo-ATS-Friendly-com-Lovable
Desafio de Projeto Final do Bootcamp da DIO

### 1. Qual problema a aplicação resolve?

Atualmente, mais de 95% das grandes e médias empresas utilizam sistemas **ATS (Applicant Tracking Systems)** — softwares que filtram, leem e ranqueiam currículos automaticamente antes de qualquer avaliação humana.

A aplicação resolve três grandes dores do candidato:

* **Falta de visibilidade sobre o filtro automático:** A maioria das pessoas envia um currículo genérico e é descartada sem saber que foi eliminada por incompatibilidade de formato ou por ausência de termos/palavras-chave exatas presentes no anúncio da vaga.
* **Formatos incompatíveis com leitura de máquinas:** Currículos criados com tabelas, colunas duplas, ícones gráficos e fontes não padrão travam os leitores ópticos dos softwares de recrutamento.
* **Insegurança sobre o que ajustar sem mentir:** Candidatos têm dificuldade de reestruturar e alinhar suas experiências reais aos requisitos exigidos sem alterar a veracidade do seu histórico profissional.

---

### 2. O mega prompt utilizado e o que mudou nele até a versão final

#### O Mega Prompt Utilizado:

O prompt final foi estruturado como uma instrução completa de arquitetura de software para o Lovable, cobrindo:

1. **Instrução de Regra de Ouro (Veracidade Ética)**;
2. **Design System & Palavra de Cores (Shadcn UI + Azul Claro, Branco e Amarelo Claro)**;
3. **Fluxo sem Autenticação/Login (100% Client-Side)**;
4. **Interface e Fluxo em 3 Passos (Entrada, Diagnóstico e Exportação)**;
5. **Mecanismo de Exportação em PDF (html2pdf.js / jsPDF)**;
6. **Lógica de Processamento e Algoritmo de Match**.

#### O que mudou do rascunho inicial até a versão final?

* **Eliminação de Dependências de Back-end e Login:** No rascunho inicial, aplicações de IA costumam incluir autenticação (Supabase/Firebase) e banco de dados. Na versão final, simplificou-se a experiência para que o usuário possa acessar, colar e baixar o PDF **sem barreiras de entrada (zero login)**, mantendo tudo em memória/localStorage.
* **Inclusão da "Regra de Ouro da Veracidade":** Adicionou-se uma diretriz algorítmica estrita para proibir a IA de fabricar experiências, cargos ou competências que o usuário não possui.
* **Garantia de Formato ATS na Exportação:** O prompt foi ajustado para detalhar exatamente *como* o PDF deve ser construído (margens, fonte única, sem elementos visuais decorativos ou colunas) para que o arquivo exportado seja realmente legível pelos robôs de recrutamento.

---

### 3. Como a análise funciona: da vaga colada até o currículo ajustado

O fluxo de processamento e inteligência da aplicação ocorre em 4 etapas sequenciais:

```
[ Entrada de Dados ] ➔ [ Tokenização e Extração ] ➔ [ Matriz de Match ] ➔ [ Reestruturação e Exportação ]

```

1. **Entrada de Dados:** O usuário cola o texto da vaga no Campo A e o seu currículo atual no Campo B.
2. **Tokenização e Normalização:** O algoritmo limpa o texto (remove conectivos/stop words como "de", "para", "com", "and") e extrai os termos relevantes da vaga (hard skills, soft skills, ferramentas, certificações e verbos de ação).
3. **Cálculo da Matriz de Match (Score %):**
* Compara a frequência e a relevância das palavras-chave da vaga com o texto do currículo original.
* Gera a nota percentual (0 a 100%) e separa os termos em **Palavras-chave Encontradas** (badges azuis/verdes) e **Palavras-chave Ausentes/Lacunas** (badges amarelas com alerta).


4. **Reestruturação e Otimização Semântica:**
* Reorganiza o resumo profissional e a ordem das competências para dar destaque imediato aos pontos do candidato que coincidem com a vaga.
* Reescreve tópicos com verbos de ação e substitui sinônimos genéricos pelas palavras-chave exatas usadas na vaga (desde que correspondam à experiência real informada).


5. **Geração do Layout ATS & Exportação em PDF:** O texto otimizado é renderizado em um contêiner A4 limpo, estruturado por seções padrão, pronto para download via PDF.

---

### 4. Que ajustes você pediu depois da primeira geração, e por quê?

Com base nas suas diretrizes de construção da aplicação, os ajustes solicitados e incorporados no megaprompt foram:

1. **Restrição de Cores Específicas (Azul Claro, Branco e Amarelo Claro):**
* *Por que:* Para garantir uma identidade visual limpa, acessível e profissional, usando o azul claro para ações primárias, o amarelo claro para sinalizar alertas/lacunas de palavras-chave sem passar sensação de erro punitivo, e o branco como base de leitura.


2. **Adoção do Shadcn UI como Design System:**
* *Por que:* O Shadcn fornece componentes de UI acessíveis, modernos e nativos em Tailwind CSS (Cards, Progress, Badges, Tabs, Textarea), perfeitos para o ecossistema do Lovable.


3. **Remoção Completa de Login/Cadastro:**
* *Por que:* Para transformar o app em uma ferramenta de execução rápida (*frictionless tool*), aumentando a retenção e o uso imediato sem atrito de registro.


4. **Exportação Direta em PDF com Padrão ATS:**
* *Por que:* Um currículo ajustado na tela não resolve o problema do usuário se ele não puder baixá-lo em um formato `.pdf` pronto para ser anexado nas plataformas de vaga (Gupy, LinkedIn, Workday).

Link para o App no Lovable: https://swift-sync-cv.lovable.app
