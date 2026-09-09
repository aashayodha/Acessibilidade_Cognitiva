# Relatório de Auditoria de Acessibilidade Cognitiva (Foco: TDAH)

Este relatório apresenta a auditoria técnica de acessibilidade cognitiva realizada no trecho de código HTML fornecido (`pagina_web_teste.html.txt`), com foco na mitigação da sobrecarga atencional para usuários com Transtorno de Déficit de Atenção com Hiperatividade (TDAH). A análise foi estruturada com base nas diretrizes WCAG 2.2 e W3C COGA.

---

### EIXO 1: Ruído Visual e Contraste

1. **Status de Conformidade:** Não Conforme
2. **Evidência no Código:**
   * **Elemento Flutuante Invasivo (Alta Distração):**
     ```html
     <div style="position: fixed; top: 20px; right: 20px; background: #ffcc00; padding: 15px; z-index: 9999; border: 2px solid red;">
         <strong>PROMOÇÃO RELÂMPAGO!</strong><br>
         <span style="color: #666; font-size: 10px;">Clique agora antes que acabe!</span>
         <button>Resgatar</button>
     </div>
     ```
   * **Baixo Contraste (Texto do Banner):** Texto em cinza (`#666` com relação de contraste de apenas **3.43:1** sobre fundo amarelo `#ffcc00`), e tamanho de fonte de `10px`, violando a WCAG SC 1.4.3 (Contraste Mínimo).
   * **Baixo Contraste (Corpo de Texto):** 
     ```html
     <p style="color: #cccccc; font-size: 13px;">
         Acompanhe abaixo os principais indicadores diários e avisos importantes referentes aos serviços disponibilizados aos cidadãos.
     </p>
     ```
     O texto cinza claro (`#cccccc` com relação de contraste de apenas **1.6:1** sobre fundo branco default) e tamanho de `13px` torna a leitura extremamente difícil.
3. **Diagnóstico de Impacto Cognitivo:**
   * **Sequestro de Atenção (Saliência Visual Involuntária):** O banner amarelo flutuante (`position: fixed`) com `z-index: 9999` e bordas vermelhas funciona como um poderoso interruptor atencional. Usuários com TDAH possuem maior suscetibilidade a estímulos distratores exógenos (captura de atenção de baixo para cima). A incapacidade de ignorar ou descartar esse elemento impede a focalização e a conclusão da tarefa principal no elemento `<main>`.
   * **Fadiga de Decodificação:** O contraste baixíssimo (`1.6:1` e `3.43:1`) e tamanhos reduzidos de fonte exigem esforço visual e cognitivo excessivo para a decodificação de grafemas. Isso sobrecarrega a memória de trabalho, gerando frustração, cansaço mental precoce e consequente abandono da página.
   * **Ansiedade e FOMO (Fear of Missing Out):** Mensagens de urgência artificial ("PROMOÇÃO RELÂMPAGO!", "antes que acabe!") induzem estresse cognitivo, prejudicando a tomada de decisões controlada.
4. **Recomendação de Correção (Código Corrigido):**
   * Substituição do banner flutuante invasivo por uma seção informativa estática e opcional (que pode ser fechada).
   * Correção dos contrastes para atender à relação mínima de **4.5:1** (ou superior) para texto normal.
   * Aumento do tamanho de fonte do parágrafo principal para `16px` para garantir legibilidade.

   ```html
   <!-- Banner promocional reestruturado como um card estático de destaque com controle de fechar (dismiss) e contrastes acessíveis -->
   <aside id="promo-banner" aria-label="Promoção" style="background: #fff8e1; color: #5d4037; padding: 15px; border-left: 5px solid #ffb300; margin-bottom: 20px; position: relative; border-radius: 4px;">
       <strong style="font-size: 18px; color: #3e2723;">Oportunidade de Destaque</strong><br>
       <p style="color: #4e342e; font-size: 14px; margin: 8px 0;">Aproveite nossos cupons de resgate para serviços selecionados do portal.</p>
       <button style="background: #e65100; color: white; border: none; padding: 8px 16px; border-radius: 4px; font-weight: bold; cursor: pointer; font-size: 14px;" aria-label="Resgatar cupom de desconto">Resgatar Cupom</button>
       <button onclick="document.getElementById('promo-banner').style.display='none'" style="position: absolute; top: 10px; right: 10px; background: none; border: none; font-size: 20px; cursor: pointer; color: #5d4037;" aria-label="Fechar anúncio">×</button>
   </aside>

   <!-- Texto principal com contraste corrigido (#333333 sobre branco tem contraste de 12.6:1) -->
   <main style="padding: 20px;">
       <h1 style="color: #111111; font-size: 28px; margin-bottom: 12px;">Últimas Atualizações do Sistema</h1>
       <p style="color: #2b2b2b; font-size: 16px; line-height: 1.6; max-width: 70ch;">
           Acompanhe abaixo os principais indicadores diários e avisos importantes referentes aos serviços disponibilizados aos cidadãos.
       </p>
   </main>
   ```

---

### EIXO 2: Controle de Movimento e Mídia

1. **Status de Conformidade:** Não Conforme
2. **Evidência no Código:**
   ```html
   <video autoplay muted loop width="100%">
       <source src="live-stream.mp4" type="video/mp4">
       Seu navegador não suporta vídeos.
   </video>
   ```
   O vídeo inicia automaticamente (`autoplay`), roda em loop infinito (`loop`) e **carece de controles nativos ou customizados (`controls`)**, impossibilitando que o usuário pause ou pare a reprodução de forma simples, violando frontalmente a WCAG SC 2.2.2 (Pausar, Parar, Ocultar). Além disso, não há implementação da diretiva `@media (prefers-reduced-motion)`.
3. **Diagnóstico de Impacto Cognitivo:**
   * **Distração Persistente Incontrolável:** Elementos visuais em movimento contínuo no campo visual periférico do usuário atuam como um "ruído estático de atenção". Como o cérebro com TDAH tem dificuldades na inibição de estímulos secundários, o movimento contínuo impede a concentração na leitura de textos adjacentes ou na realização de formulários, gerando cansaço imediato.
   * **Perda de Controle de Agentes Ambientais:** A ausência de um botão visível de pausa retira do usuário a autonomia sobre o conteúdo que consome, gerando frustração e sobrecarga sensorial.
4. **Recomendação de Correção (Código Corrigido):**
   * Inclusão do atributo `controls` e remoção do `autoplay` padrão (ou fornecimento de pausa automática respeitando as preferências do sistema operacional do usuário através de CSS/JavaScript).
   * Uso da propriedade `@media (prefers-reduced-motion: reduce)` para assegurar que animações e loops sejam pausados automaticamente para usuários que indicaram preferência por movimento reduzido.

   ```html
   <!-- Seção de vídeo reestruturada com controles visíveis e comportamento não-invasivo -->
   <section style="margin: 20px 0; border: 1px solid #ccc; border-radius: 8px; padding: 15px; background: #fafafa;">
       <h3 style="margin-top: 0; color: #111;">Transmissão Ao Vivo</h3>
       <!-- Removido autoplay para evitar surpresa atencional; adicionados controles manuais -->
       <video id="live-video" controls muted width="100%" style="border-radius: 4px; background: #000;">
           <source src="live-stream.mp4" type="video/mp4">
           Seu navegador não suporta a reprodução de vídeos.
       </video>
   </section>

   <style>
       /* Respeito às preferências de movimento reduzido do sistema do usuário */
       @media (prefers-reduced-motion: reduce) {
           video {
               transition: none !important;
               animation: none !important;
           }
       }
   </style>
   <script>
       // Garantia programática de que o vídeo não dará play automático caso o usuário prefira movimento reduzido
       const motionQuery = window.matchMedia('(prefers-reduced-motion: reduce)');
       const videoElement = document.getElementById('live-video');
       if (motionQuery.matches && videoElement) {
           videoElement.removeAttribute('autoplay');
           videoElement.pause();
       }
   </script>
   ```

---

### EIXO 3: Layout Previsível e Estrutura Semântica

1. **Status de Conformidade:** Não Conforme
2. **Evidência no Código:**
   * **Substituição de Tags de Navegação Semântica por DIVs:**
     ```html
     <div style="background: #333; color: white; padding: 10px;">
         <span>Início</span> | <span>Serviços</span> | <span>Contato</span>
     </div>
     ```
     O menu de navegação é representado por uma `<div>` genérica e elementos `<span>` puros que não são links (`<a>`), não possuem semântica de navegação (`<nav>`) nem estrutura de cabeçalho (`<header>`).
   * **Falta de Focabilidade do Teclado:** Os elementos de navegação não são interativos (não contêm `href` ou `tabindex`), impedindo a navegação por teclado e a identificação por tecnologias assistivas (violando as WCAG SC 3.2.3 - Navegação Consistente e SC 2.1.1 - Teclado).
3. **Diagnóstico de Impacto Cognitivo:**
   * **Desorientação Espacial e Quebra de Expectativas:** A inconsistência de layout e a falta de tags semânticas estruturadas rompem os modelos mentais previsíveis que usuários com TDAH dependem para mapear e entender o site de forma rápida. Sem uma estrutura previsível (`header`, `nav`, `main`), o usuário gasta recursos cognitivos extras tentando descobrir onde as seções estão localizadas.
   * **Friction de Navegação por Teclado:** Usuários com TDAH que também possuem dificuldades motoras finas associadas ou que dependem do teclado para manter o ritmo de foco perdem o fluxo de atenção se a navegação não responde de forma visual e previsível às teclas de atalho (como Tabulação).
4. **Recomendação de Correção (Código Corrigido):**
   * Reestruturação usando cabeçalho (`<header>`), navegação (`<nav>`), listas estruturadas (`<ul>`, `<li>`) e links (`<a>`) totalmente operáveis por teclado e estilizados com estados claros de foco (`:focus-visible`).

   ```html
   <!-- Cabeçalho e navegação semânticos e perfeitamente acessíveis -->
   <header style="background: #1a1a1a; padding: 15px 20px;">
       <nav aria-label="Navegação Principal">
           <ul style="list-style: none; margin: 0; padding: 0; display: flex; gap: 20px;">
               <li>
                   <a href="#inicio" style="color: #ffffff; text-decoration: none; font-weight: bold; font-size: 16px; padding: 8px 12px; border-radius: 4px; transition: background 0.2s;" onfocus="this.style.outline='3px solid #ffcc00'" onblur="this.style.outline='none'">
                       Início
                   </a>
               </li>
               <li>
                   <a href="#servicos" style="color: #ffffff; text-decoration: none; font-weight: bold; font-size: 16px; padding: 8px 12px; border-radius: 4px; transition: background 0.2s;" onfocus="this.style.outline='3px solid #ffcc00'" onblur="this.style.outline='none'">
                       Serviços
                   </a>
               </li>
               <li>
                   <a href="#contato" style="color: #ffffff; text-decoration: none; font-weight: bold; font-size: 16px; padding: 8px 12px; border-radius: 4px; transition: background 0.2s;" onfocus="this.style.outline='3px solid #ffcc00'" onblur="this.style.outline='none'">
                       Contato
                   </a>
               </li>
           </ul>
       </nav>
   </header>
   ```

---

### EIXO 4: Progresso, Estados e Redundância de Entrada

1. **Status de Conformidade:** Parcialmente Conforme
2. **Evidência no Código:**
   ```html
   <form style="background: #f9f9f9; padding: 15px;">
       <label>Pesquisar no Portal:</label><br>
       <input type="text" name="q" placeholder="Digite o termo..." style="width: 80%; padding: 8px;"><br><br>
       <button type="submit" style="background: #0044cc; color: white; padding: 8px 15px;">Buscar</button>
   </form>
   ```
   * **Desconexão de Rótulo e Campo:** A tag `<label>` não possui o atributo `for` associado ao `id` do `<input>`, prejudicando a acessibilidade para leitores de tela e a área de clique para usuários (violando WCAG SC 3.3.2 - Rótulos ou Instruções).
   * **Ausência de Autocompletar / Persistência:** Não há declaração de `autocomplete` no campo de texto para facilitar o preenchimento automático de pesquisas recorrentes ou recuperação de termos passados (violando WCAG SC 3.3.7 - Entrada Redundante).
3. **Diagnóstico de Impacto Cognitivo:**
   * **Sobrecarga na Memória de Trabalho:** Se o usuário com TDAH digitar um termo e o formulário falhar ou recarregar sem persistir os dados digitados ou sem oferecer autocompletar, ele terá que refazer o processo cognitivo de digitação. Isso resulta em fadiga da atenção ativa e propensão ao erro de digitação secundária.
   * **Falta de Foco Guiado:** Rótulos desconectados de seus campos reduzem a facilidade de interação física e cognitiva com o controle, exigindo maior precisão motora e mental para ativar o campo de pesquisa.
4. **Recomendação de Correção (Código Corrigido):**
   * Vincular explicitamente o `<label>` ao `<input>` usando `for` e `id`.
   * Incluir `autocomplete="search"` para ativar a persistência e autocompletar do navegador.
   * Otimizar o estilo do botão de envio com indicadores claros de estado e foco visual.

   ```html
   <!-- Formulário de pesquisa otimizado para atenção sustentada e preenchimento ágil -->
   <form role="search" aria-label="Pesquisa de Conteúdo" style="background: #f5f5f5; border: 1px solid #e0e0e0; padding: 20px; border-radius: 8px; max-width: 600px;">
       <div style="display: flex; flex-direction: column; gap: 8px;">
           <!-- Label conectado por ID com tamanho confortável -->
           <label for="search-input" style="font-weight: bold; color: #111111; font-size: 16px;">
               Pesquisar no Portal:
           </label>
           
           <div style="display: flex; gap: 10px; width: 100%;">
               <input 
                   type="search" 
                   id="search-input" 
                   name="q" 
                   placeholder="Ex: certidões, agendamento..." 
                   autocomplete="search" 
                   style="flex: 1; padding: 12px; font-size: 16px; border: 2px solid #757575; border-radius: 4px; box-sizing: border-box;"
                   aria-required="true"
               >
               <button 
                   type="submit" 
                   style="background: #0044cc; color: #ffffff; padding: 12px 24px; border: none; border-radius: 4px; font-size: 16px; font-weight: bold; cursor: pointer; transition: background 0.2s;"
                   onmouseover="this.style.background='#0033aa'"
                   onmouseout="this.style.background='#0044cc'"
               >
                   Buscar
               </button>
           </div>
       </div>
   </form>
   ```

---

## Conclusão da Auditoria Estática

O código original analisado apresentou um nível crítico de **Não Conformidade** na maior parte dos eixos de acessibilidade cognitiva. A combinação de ruído visual flutuante (Eixo 1), mídias sem controle com reprodução contínua (Eixo 2), quebra de padrões semânticos de navegação (Eixo 3) e fragilidade no design de formulários de persistência e suporte a erros (Eixo 4) cria uma barreira expressiva que gera fadiga rápida e dispersão para usuários com TDAH.

A implementação das recomendações de correção sugeridas aproxima substancialmente o portal dos padrões ideais de usabilidade descritos pelo W3C COGA e pelas WCAG 2.2, promovendo uma navegação focada, limpa, previsível e acolhedora para a neurodiversidade.
