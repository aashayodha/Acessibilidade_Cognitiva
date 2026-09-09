Acessibilidade Digital: Auditoria e Conformidade Cognitiva para TDAH
Este repositório armazena o ciclo prático de auditoria em interfaces web para usuários com Transtorno do Déficit de Atenção e Hiperatividade (TDAH). Utilizando a matriz prescritiva e o checklist de 12 itens fundamentados na pesquisa acadêmica sobre carga cognitiva e acessibilidade, o espaço documenta códigos HTML/CSS/JS originais (antes) e suas respectivas versões corrigidas (depois).
Sobre o Repositório
O objetivo central é traduzir diretrizes teóricas de acessibilidade cognitiva (W3C/COGA e WCAG 2.2) em artefatos práticos e verificáveis, aplicando prompts estruturados baseados na norma ISO/IEC/IEEE 26514:2022 para auditoria assistida por Modelos de Linguagem de Grande Escala (LLM).
Eixos Operacionais de Auditoria
Eixo 1 - Redução de Ruído Visual e Carga Perceptiva: Mitigação de pop-ups não solicitados, sobreposições excessivas (z-index) e garantia de contraste cromático mínimo (4,5:1).
Eixo 2 - Controle de Movimento e Mídia Acessível: Validação de @media (prefers-reduced-motion: reduce) e controle de reprodução automática (autoplay) em mídias.
Eixo 3 - Layout Previsível e Consistência: Manutenção da estabilidade estrutural do DOM (header, nav, main) e rotulagem textual acessível.
Eixo 4 - Visualização de Progresso e Tarefas: Implementação de indicadores de etapa (aria-current="step") e persistência local de dados para evitar preenchimento redundante.
Estrutura dos Arquivos
Arquivo / Pasta
Descrição
 
/auditoria-original/
Códigos fonte iniciais contendo barreiras atencionais e falhas de usabilidade cognitiva.
/pagina-corrigida/
Códigos refatorados após a aplicação da matriz de prompts e do checklist cognitivo.
/prompts/
Blocos de comandos executáveis para inspeção estática por IA.

Como Utilizar
Navegue pelas pastas do repositório para inspecionar os exemplos práticos de código antes e depois da refatoração voltada à inclusão digital e à gestão da carga cognitiva.

## Links Rápidos para Auditoria Código HTML
* [Página Web Corrigida](pagina_web_corrigida.html)
* [Página Web de Teste (Original)](pagina_web_teste.html)
* [Relatório de Auditoria (IA)](relatorio_auditoria_ia.md)
* [Relatório de Auditoria (Depois)](relatorio_auditoria_depois.md)

  ## Links Rápidos para Auditoria Visualização Páginas Web
* [Página Web Corrigida](https://aashayodha.github.io/Acessibilidade_Cognitiva/pagina_web_corrigida.html)
* [Página Web de Teste (Original)](https://aashayodha.github.io/Acessibilidade_Cognitiva/pagina_web_teste.html)

## Link Relatório de Auditoria de Originalidade e Plágio
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/14i8g_A3N8hbtjzTmbYNqHjEJdELe2E3R?usp=sharing)
